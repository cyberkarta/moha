# Mobile App Testing Guide

## Issues and Steps for Testing
Source: https://www.youtube.com/watch?v=vz9eAUzsVeE

Common issues:
- App permissions
- Configuration flaws
- Improper data storage
- Allowing 301 redirects
- Insecure authentication
- Client code quality
- Insecure authorization
- Code tampering

Testing:
- Define goal of the audit
	- Validate app permission
	- In app config
	- Authentication and authorization
	- Authorization token / cookie
	- Data storage mechanism

- Threat analysis and modelling (using tools like ADB, MobSF, iMas)
	- Review architecture
	- Check application resources
	- Review third-party interactions
	- Kill threat agents
	- Penetration of the vulnerabilities

Tools:
- **ADB** Android Debug Bridge, assess and debug mobile apps. ADB is a client-server program. It is limited to Android OS.
- **MobSF** Mobile Security Framework, is an automated security testing framework for Android and iOS. It performs static and dynamic analysis for mobile app security.
- **iMAS**, iOS Mobile Application Security is iOS security testing framework, it works nice to detect vulnerabilities related to security controls, CWE, system Passcode, jailbreak, debugger/run-time, flash storage, and keychain.

Exploitation tools
- **QARK** Quick Android Review Kit, automated Android pen-testing tool. Scan all components in mobile app, and detect misconfigurations and threats. https://github.com/linkedin/qark, guide: https://medium.com/@_foso_/android-penetration-testing-with-qark-a7debfc31d0b
- OWAP ZAP
- Mitmproxy

