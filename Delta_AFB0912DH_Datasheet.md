# Delta AFB0912DH Fan Datasheet
## Reverse Engineered from Bench Testing

---

## GENERAL SPECIFICATIONS

**Manufacturer:** Delta Electronics Inc.  
**Model Number:** AFB0912DH  
**Application:** HP ProLiant ML350 G6 Server (HP P/N: 511774-001 / 508110-001)  
**Fan Type:** DC Brushless Axial Flow Fan  
**Bearing Type:** Dual Ball Bearing  

---

## MECHANICAL SPECIFICATIONS

| Parameter | Value |
|-----------|-------|
| **Dimensions** | 92mm × 92mm × 25mm |
| **Mounting Holes** | Standard 92mm pattern |
| **Weight** | ~150g (estimated) |
| **Frame Material** | Plastic with integrated shroud |
| **Airflow Direction** | Standard axial (marked on housing) |

---

## ELECTRICAL SPECIFICATIONS

### Power Requirements
| Parameter | Value | Notes |
|-----------|-------|-------|
| **Rated Voltage** | 12V DC | |
| **Voltage Range** | 10.8V - 13.2V | Typical ±10% tolerance |
| **Rated Current** | 2.5A | Label specification |
| **Actual Maximum Current** | 1.67A | Measured at full speed |
| **Maximum Power** | 20W | Measured at full speed |

### Performance
| Parameter | Value | Notes |
|-----------|-------|-------|
| **Rated Speed** | 8,600 RPM | At full power |
| **Speed Control Range** | Variable | Via PWM (see control specs) |
| **Estimated Airflow** | 110-120 CFM | At full speed |
| **Noise Level** | 50-55 dBA | Estimated at full speed |
| **Life Expectancy** | 50,000-70,000 hours | Dual ball bearing spec |

---

## CONNECTOR & PINOUT

### Physical Connector
- **Type:** Proprietary HP 5-pin housing (4 wires populated)
- **Pitch:** 2.54mm (0.1")
- **Keying:** Mechanical polarization via housing design

### Pin Configuration & Wire Colors

**WARNING: CRITICAL: This fan uses NON-STANDARD wire color coding!**

| Pin | Wire Color | Function | Signal Type |
|-----|------------|----------|-------------|
| 1 | **BLACK** | Ground (GND) | Power ground |
| 2 | **RED** | +12V DC Power | DC power input |
| 3 | **YELLOW** | Tachometer Output | Open collector, 2 pulses/rev |
| 4 | **GREEN** | PWM Control Input | 25 kHz square wave |
| 5 | Empty | Not connected | N/A |

**Note:** Pin 5 physically exists in the connector housing but has no wire.

---

## PWM CONTROL SPECIFICATIONS

### PWM Input Signal (Green Wire)

| Parameter | Value | Notes |
|-----------|-------|-------|
| **Frequency** | 25 kHz ±10% | Standard Intel 4-wire spec |
| **Acceptable Range** | 21 kHz - 28 kHz | |
| **Signal Voltage** | 0V to 5V | TTL logic level |
| **Logic Low** | 0V - 0.8V | |
| **Logic High** | 3.5V - 5V | |
| **Input Impedance** | High-Z | Internally pulled up |

### PWM Control Characteristics

**WARNING: INVERTED PWM LOGIC - NON-STANDARD!**

| Duty Cycle | Fan Speed | Power Level |
|------------|-----------|-------------|
| **1%** | **MAXIMUM** | **FULL POWER** |
| 25% | High | ~75% power |
| 50% | Medium | ~50% power |
| 75% | Low | ~25% power |
| **99%** | **MINIMUM** | **LOWEST POWER** |

**IMPORTANT:** This fan uses inverted PWM logic where:
- **LOW duty cycle = HIGH speed/power**
- **HIGH duty cycle = LOW speed/power**

This is opposite of most standard PC fans!

---

## TACHOMETER OUTPUT SPECIFICATIONS

### Tach Signal (Yellow Wire)

| Parameter | Specification | Measured (Failed Fan) |
|-----------|---------------|----------------------|
| **Signal Type** | Open collector/drain | Same |
| **Pulses per Revolution** | 2 | Confirmed |
| **Normal Output Voltage** | 3V - 5V peak | 200mV (FAILED) |
| **Output Frequency** | ~286 Hz at 8,600 RPM | Varies with speed |
| **Pull-up Required** | Yes (on motherboard) | Yes |

**Normal Operation:**  
- Signal toggles between 0V and ~5V
- 2 pulses per revolution
- Clean square wave
- At 8,600 RPM: 8,600 ÷ 60 × 2 = 286.7 Hz

**Failure Mode Observed:**  
- Weak signal: ~200mV peak instead of 3-5V
- Server reports "Fan Failed" even though motor runs
- Indicates failing Hall sensor or output driver circuit

---

## WIRING DIAGRAM

```
Fan Connector (Orange Housing - HP Proprietary 5-pin)
Looking at connector from wire side:

Pin Layout:  1   2   3   4   5
             |   |   |   |   (empty)
             |   |   |   |
             |   |   |   +-- GREEN  - PWM Input (25kHz, 0-5V)
             |   |   +------ YELLOW - Tach Output (2 pulses/rev)
             |   +---------- RED    - +12V DC Power
             +-------------- BLACK  - Ground

Pin 5: Physical position exists but no wire connected
```

---

## POWER SUPPLY CONNECTION

### Bench Testing Setup

```
Power Supply:
  (+) ------ RED wire    (12V DC)
  (-) ------ BLACK wire  (Ground)

Function Generator (for PWM control):
  Output --- GREEN wire (25kHz square wave, 0-5V)
  Ground --- BLACK wire (common ground)

Oscilloscope (to monitor tach):
  Ch1 ------- YELLOW wire (tach output)
  Ground ---- BLACK wire
```

### Minimum Connections for Operation
- **RED** to +12V
- **BLACK** to Ground
- **GREEN** to PWM signal (or leave floating for ~50% speed)

Fan will NOT start reliably without valid PWM signal on healthy units.

---

## FAILURE MODES & DIAGNOSTICS

### Common Failure: Motor Controller Starting Circuit

**Symptoms:**
- Fan will NOT self-start at any PWM duty cycle (1% to 99%)
- Requires manual spin to initiate rotation
- Runs smoothly once started
- Responds to PWM speed control after manual start
- Weak tachometer signal (~200mV instead of 3-5V)

**Root Cause:**
- Internal brushless motor controller IC failure
- Starting circuit cannot generate initial commutation
- Tach output circuit also degraded

**Diagnosis Method:**
1. Apply 12V DC to RED/BLACK wires
2. Apply 25kHz PWM signal at various duty cycles to GREEN wire
3. Observe if fan self-starts
4. Measure tach signal on YELLOW wire with oscilloscope

**Expected Results (Healthy Fan):**
- Self-starts at any duty cycle 1-99%
- Tach output: 3-5V peak, ~286Hz at full speed
- Clean square wave on tach output

**Failed Fan Results:**
- No self-start at any duty cycle
- Manual spin required to start
- Tach output: <1V peak (typically 200mV observed)
- Weak/degraded square wave

**Conclusion:** Replace fan - internal electronics failure

---

## REPLACEMENT PARTS

### HP Part Numbers
- **HP Spare:** 511774-001
- **HP Assembly:** 508110-001

### Delta Model Variants
- AFB0912DH (standard model)
- AFB0912DH-A (variant)

### Compatible Applications
- HP ProLiant ML350 G6
- HP ProLiant ML330 G6
- Other HP G6 series tower servers

---

## SAFETY & COMPLIANCE

**Certifications:** UL Listed  
**Operating Temperature:** 0°C to +70°C  
**Storage Temperature:** -40°C to +85°C  
**Humidity:** 5% to 95% RH, non-condensing  

---

## IMPORTANT NOTES

### CRITICAL WARNINGS

1. **NON-STANDARD WIRE COLORS**  
   This fan does NOT follow typical PC fan color coding!
   - RED = Power (usually YELLOW on PC fans)
   - YELLOW = Tach (usually GREEN on PC fans)
   - GREEN = PWM (usually BLUE on PC fans)

2. **INVERTED PWM LOGIC**  
   Low duty cycle = HIGH speed (opposite of most fans!)

3. **NOT HOT-SWAPPABLE**  
   Power down server before replacing

4. **PROPRIETARY CONNECTOR**  
   5-pin HP connector - not compatible with standard 4-pin PC fan headers without adapter

5. **SERVER THERMAL PROTECTION**  
   Do not operate server with failed fan - risk of overheating and component damage

---

## BENCH TESTING RESULTS

**Test Equipment Used:**
- Rigol DP832 Power Supply
- Rigol Oscilloscope
- Function Generator (25kHz)
- Fluke Multimeter

**Test Date:** January 27, 2025  
**Test Engineer:** LANgineers Inc.  
**Test Location:** Field diagnostic bench

**Findings:**
- Fan exhibits starting circuit failure
- Tach output degraded to ~200mV (normal: 3-5V)
- Motor and bearings mechanically sound
- PWM speed control functional once manually started
- Maximum power draw: 20W at full speed
- Inverted PWM logic confirmed (1% = full speed)

**Recommendation:** Replace fan assembly due to internal motor controller failure

---

## ADDITIONAL RESOURCES

### Purchase Links
Available from:
- Amazon (search: HP 511774-001 or Delta AFB0912DH)
- eBay (search: HP ML350 G6 fan or 511774-001)
- Server parts suppliers (ServerWorlds, Buffalo Computer Parts, etc.)

**Typical Price Range:** $26 - $55 USD (refurbished/used)

### Online Documentation
- HP ML350 G6 Service Guide
- Delta Electronics official website
- Pinout diagrams: pinoutguide.com

---

## REVISION HISTORY

**Version 1.0** - January 27, 2025
- Initial reverse-engineered datasheet
- Based on bench testing and physical inspection
- Confirmed pinout, PWM characteristics, and failure modes

---

## DISCLAIMER

This datasheet was created through reverse engineering and bench testing.  
While every effort has been made to ensure accuracy, this is NOT an official  
Delta Electronics or HP document. Use this information at your own risk.

For official specifications, contact:
- Delta Electronics Inc.
- HP Enterprise Support

---

**Document Created By:** LANgineers Inc.  
**Test Technician:** Albert C.  
**Date:** January 27, 2025  
**Location:** Burlingame, CA  

---

*This datasheet is provided for educational and diagnostic purposes.*  
*Feel free to share, but please credit the source.*

**YouTube Channel:** [Your Channel Name Here]  
**Company:** LANgineers Inc. - California Licensed Telecommunications Contractor #1143558

---

END OF DATASHEET
