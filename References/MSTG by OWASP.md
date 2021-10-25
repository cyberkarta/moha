## Mobile App Taxonomy
### Native App
Native app: application that is built by the native language of the OS, it has better reliability and performance.
iOS = Objective-C or Swift
Android = Kotlin and Java

Single code for both platform, these framework can also be considered as native apps (performance equivalent to native applications)
- Xamarin
- Flutter
- React Native

### Web App
Run on top of a device's browser and usually developed in HTML5. Because run within the browser/sandboxed, they usually lack in performance in comparison of native app. The biggest advantage is reduced development and maintenance costs.

### Hybrid App
Executes like a native app, but majority of the process rely on web technologies using embedded web browser (web view). Frameworks:
- Apache Cordova
- Framework 7
- Ionic
- JQuery Mobile
- Native Script
- Onsen UI
- Sencha TOuch

### Progressive Web App (PWA)
Load like regular web pages, but its possible to work offline and access mobile device hardware. A web app manifest (JSON file) can be used to configure the behavior of the app after installation.


## Security Testing
A mobile app security test is usually part of a larger security assessment or penetration test that encompasses the client-server architecture and server-side APIs used by the mobile app.
- Black-box testing, testing without any information about the tested app, represents real attacker
- White-box testing, the tester has full knowledge of the app (the source code, documentation, and diagrams), faster testing and granular test cases.
- Gray-box, in between black-box testing and white-box testing. Usually the tester get credentials only and other information is intended to be discovered.

Tips:
- it is better to request the source code so that you can use the testing time as efficiently as possible. White-box test is the way to go if the app hasn't been tested before.
- Even though decompiling is straightforward on Android, the source code may be obfuscated. It takes time to de-obfuscate it.

### Vulnerability Analysis
[_Static vs Dynamic](_Static%20vs%20Dynamic.md)
Looking for vulnerabilities in an app, it can be done manually or automatically using scanner.

#### Static Application Security Testing (SAST)
Examining an application's component without executing them, by analyzing the source code either manually or automatically.

**Manual code review**, manually analyzing the mobile application's source code. Can also be done using 'grep' command or even line-by-line examination of the source code. IDE (Integrated Development Environment) often provide basic code review functions and can be extended with various tools.

Common approach: manual code analysis entails identifying key security vulnerability indicators by searching for certain APIs and keywords, such as database-related method calls like "executeStatement" or "executeQuery", these words are good starting points.

Advantage: good for identifying vulnerabilities in the business logic, standards violations, and design flaws.

Notes: 
- code review requires an expert code reviewer who is proficient in both the language and the frameworks used for the mobile application.
- Full code review can be a slow, tedious, time-consuming process for the reviewer, especially given large code bases with many dependencies.


**Automated Source Code Analysis**
Using analysis tools can be speed up the review process of Static Application Security Testing (SAST). They check the source code for compliance with a predefined set of rules of industry best practices.

 