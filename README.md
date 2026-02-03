# Delta AFB0912DH Fan Datasheet

Reverse-engineered datasheet for the Delta AFB0912DH DC brushless fan, commonly used in HP ProLiant ML350 G6 servers (HP P/N: 511774-001, 508110-001).

![Delta AFB0912DH Fan](https://img.shields.io/badge/Status-Tested%20%26%20Documented-success)
![HP ProLiant ML350 G6](https://img.shields.io/badge/Application-HP%20ProLiant%20ML350%20G6-blue)
![License](https://img.shields.io/badge/License-CC0%201.0-lightgrey)

---

## ⚠️ CRITICAL WARNINGS

This fan uses **NON-STANDARD wire color coding** that differs from typical PC fans:

| Wire Color | Function | Standard PC Fan Color |
|------------|----------|----------------------|
| **RED** | +12V Power | ❌ Usually YELLOW |
| **YELLOW** | Tachometer Output | ❌ Usually GREEN |
| **GREEN** | PWM Control Input | ❌ Usually BLUE |
| **BLACK** | Ground | ✅ Standard |

### Inverted PWM Logic

This fan also uses **inverted PWM control**:
- **1% duty cycle = FULL SPEED** (maximum power)
- **99% duty cycle = MINIMUM SPEED** (lowest power)

This is the **opposite** of most standard PC fans!

---

## 📄 Documentation Files

- **[PDF Datasheet](Delta_AFB0912DH_Datasheet.pdf)** - Print-friendly, comprehensive technical documentation
- **[Markdown Version](Delta_AFB0912DH_Datasheet.md)** - Editable format with full specifications

---

## 🔧 Key Specifications

| Parameter | Value |
|-----------|-------|
| **Model** | Delta AFB0912DH |
| **Size** | 92mm × 92mm × 25mm |
| **Voltage** | 12V DC |
| **Current** | 2.5A (rated), 1.67A (measured at full speed) |
| **Power** | 20W maximum |
| **Speed** | 8,600 RPM (at full power) |
| **Bearing** | Dual Ball Bearing |
| **Connector** | HP Proprietary 5-pin (4 wires populated) |
| **PWM Frequency** | 25 kHz |

---

## 🔍 What's Included

### Complete Pinout Documentation
- Verified wire colors and pin functions
- Connector diagrams and wiring schematics
- Bench test setup configurations

### PWM Control Specifications
- Frequency: 25 kHz (Intel spec)
- Signal levels: 0-5V TTL logic
- Inverted duty cycle operation documented
- Speed control characteristics

### Tachometer Output Details
- Normal operation: 3-5V peak, 2 pulses/revolution
- Failure mode symptoms and diagnostic procedures
- Signal measurement guidelines

### Failure Mode Analysis
- Common failure: Motor controller starting circuit
- Diagnostic procedures with oscilloscope
- Symptoms: Won't self-start, weak tach signal
- Troubleshooting flowchart

### Replacement Information
- HP part numbers: 511774-001, 508110-001
- Compatible server models
- Purchase sources and typical pricing

---

## 🎬 YouTube Video

**Watch the full diagnostic and reverse engineering process:**

📺 [LANgineers YouTube Channel](https://www.youtube.com/@LANgineers)

*Video showing oscilloscope testing, pinout verification, and failure mode analysis*

---

## 🛠️ Testing Methodology

This datasheet was created through systematic bench testing using:

- **Rigol DP832** programmable DC power supply
- **Rigol Oscilloscope** for signal analysis
- **Function Generator** for PWM signal generation (25 kHz)
- **Fluke Multimeter** for voltage/current measurements

### Tests Performed:
1. ✅ Pinout verification with continuity testing
2. ✅ Power consumption measurement at various speeds
3. ✅ PWM duty cycle vs. speed characterization
4. ✅ Tachometer signal analysis (frequency, amplitude, waveform)
5. ✅ Starting circuit failure diagnosis
6. ✅ Bearing and motor mechanical inspection

**Test Date:** January 27, 2025  
**Location:** Burlingame, CA

---

## 🏢 About LANgineers Inc.

**LANgineers Inc.** is a California-licensed telecommunications contractor specializing in:
- VoIP phone systems
- Surveillance camera installations
- Access control systems
- Network infrastructure

**California Contractor License:** #1143558  
**Location:** Burlingame, CA (San Francisco Bay Area)

### Connect with Us:
- 📺 [YouTube: LANgineers](https://www.youtube.com/@LANgineers)
- 🌐 Website: *(contact for info)*
- 📞 Phone: 650-692-2001 x101

---

## 📋 Use Cases for This Documentation

This datasheet is useful for:

- 🔧 **IT Professionals** troubleshooting HP ProLiant server fans
- 🏭 **Data Center Technicians** performing server maintenance
- 🎓 **Engineering Students** learning about brushless DC motor control
- 🛠️ **Makers/Hobbyists** repurposing server fans for custom projects
- 📚 **Technical Documentation** when official datasheets aren't available

---

## ⚖️ License & Usage

This documentation is released under **CC0 1.0 Universal (Public Domain)**

You are free to:
- ✅ Use commercially
- ✅ Modify and redistribute
- ✅ Use in private projects
- ✅ Use without attribution (though attribution is appreciated!)

**Disclaimer:** This is reverse-engineered documentation, not official Delta Electronics or HP documentation. Use at your own risk. For official specifications, contact Delta Electronics or HP Enterprise.

---

## 🤝 Contributing

Found an error? Have additional information? Contributions are welcome!

- Open an issue to report inaccuracies
- Submit a pull request with corrections or enhancements
- Share your own test results or findings

---

## 📞 Contact

**For technical questions or professional services:**

**LANgineers Inc.**  
1799 Bayshore HWY STE 230  
Burlingame, CA 94010

Phone: 650-692-2001 x101  
Fax: 650-692-2110

---

## 🌟 Support This Work

If you found this documentation helpful:

- ⭐ **Star this repository** on GitHub
- 📺 **Subscribe to [LANgineers on YouTube](https://www.youtube.com/@LANgineers)**
- 💬 **Share with colleagues** who work with server hardware
- 🎥 **Watch and like** the related YouTube video

---

## 📚 Related Resources

- [HP ProLiant ML350 G6 Service Guide](https://support.hpe.com/hpesc/public/docDisplay?docId=emr_na-c01955343)
- [Delta Electronics Official Website](https://www.delta-fan.com/)
- [Intel 4-Wire PWM Specification](https://www.intel.com/content/www/us/en/support/articles/000005852/processors.html)

---

**Last Updated:** February 3, 2025  
**Document Version:** 1.0  
**Repository Maintained By:** LANgineers Inc.

---

*Helping the tech community through detailed reverse engineering and documentation.* 🔧
