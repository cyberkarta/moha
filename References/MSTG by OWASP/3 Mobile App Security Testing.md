# Security Testing
A mobile app security test is usually part of a larger security assessment or penetration test that encompasses the client-server architecture and server-side APIs used by the mobile app.
- Black-box testing, testing without any information about the tested app, represents real attacker
- White-box testing, the tester has full knowledge of the app (the source code, documentation, and diagrams), faster testing and granular test cases.
- Gray-box, in between black-box testing and white-box testing. Usually the tester get credentials only and other information is intended to be discovered.

Tips:
- it is better to request the source code so that you can use the testing time as efficiently as possible. White-box test is the way to go if the app hasn't been tested before.
- Even though decompiling is straightforward on Android, the source code may be obfuscated. It takes time to de-obfuscate it.

## Vulnerability Analysis
[_Static vs Dynamic](../_Static%20vs%20Dynamic.md)
Looking for vulnerabilities in an app, it can be done manually or automatically using scanner.

### Static Application Security Testing (SAST)
Examining an application's component without executing them, by analyzing the source code either manually or automatically.

**Manual code review**, manually analyzing the mobile application's source code. Can also be done using 'grep' command or even line-by-line examination of the source code. IDE (Integrated Development Environment) often provide basic code review functions and can be extended with various tools.

Common approach: manual code analysis entails identifying key security vulnerability indicators by searching for certain APIs and keywords, such as database-related method calls like "executeStatement" or "executeQuery", these words are good starting points.

Advantage: good for identifying vulnerabilities in the business logic, standards violations, and design flaws.

Notes: 
- code review requires an expert code reviewer who is proficient in both the language and the frameworks used for the mobile application.
- Full code review can be a slow, tedious, time-consuming process for the reviewer, especially given large code bases with many dependencies.


**Automated Source Code Analysis**
Using analysis tools can be speed up the review process of Static Application Security Testing (SAST). They check the source code for compliance with a predefined set of rules of industry best practices, then display a list of findings or warnings and flags for all detected violations. 

Some static analysis tools run against the compiled app only, it is better to fed original source code and run as live-analysis plugins in the IDE.





