# Mobile Top 10 2016
Source: https://owasp.org/www-project-mobile-top-10/2016-risks

## M1: Improper Platform Usage
Misuse of a platform or failure to use platform security controls.
- Android intents
- Platform permissions
- Misuse of touchID
- Keychain
- Other security controls that is part of the mobile operating system.

Vectors: Exposed API calls

Detection: API call that is consumed by the mobile app because of insecure coding. Through the mobile interface, an adversary is able to feed malicious inputs or unexpected sequences of events to the vulnerable endpoint.

Risk
1. Mobile app that does not follow best practices recommended by documentation.
2. Not all best practices are documented in guidance, there are common best practices too.
3. Unintentional misuse. Some apps intend to do the right thing, but actually get some part of the implementation wrong. (simple bug, wrong flag on API calls, misunderstanding about how the protections work)

Example attack scenarios:
**App local storage instead of keychain.** iOS keychain is a secure storage facility for app and system data. YOu should use it to store any small data that has security significance (session keys, passwords, device enrollment data, etc)

Vulnerabilities:
- Injection (SQL, XSS, command)
- Logic flaws
- Weak authentication/broken authentication
- Weak or no session management
- Session fixation
- Sensitive data transmitted using GET method
- Default content and administrative interfaces
- Session management flaws
- Access control vulnerabilities
- Local and remote file inclusion

## M2: Insecure Data Storage
Attack on lost/stolen mobile device or using malware, or another repackaged app. It occurs when development teams assume that users or malware will not have access to a mobile device's filesystem and subsequent sensitive information in data-stores.

App on risk:
- Poor encryption library
- Rooting and jailbreaking to circumvents any encryption protections.

Impacts:
- Identity theft
- Privacy
- Fraud
- Reputation damage
- External policy violation
- Material loss

Impacted location
- SQL databases
- Log files
- XML data stores of manifest files [Android Basic](Android%20Basic.md)
- Binary data stores
- Cookie stores
- SD card
- Cloud synced

Unintended data leakage
- The OS
- Frameworks
- Compiler environment
- New hardware
- Rooted or jailbroken devices

Underdocumented internal processes:
- How OS caches data, images, key-presses, logging, buffers
- How development framework caches data, images, key-presses, logging, buffers
- The way of data ad, analytical, social or enablement frameworks cache data, images, key-presses, logging, buffers

Prevention: See how the APIs handle assets:
- URL caching (request and response)
- Keyboard key caching
- Copy and paste buffer caching
- Application backgrounding
- Intermediate data
- Logging
- HTML5 data storage
- Browser cookie objects
- Analytical data sent to third parties

Example: iGoat as fake bank app to steal credentials.sqlite

## M3: Insecure Communication
Vulnerabilities when data is exchanged from client to server vice versa. Threat agents:
- Adversary that shares local network (compromised or monitored wifi)
- Carrier or network devices (routers, cell towers, proxy's, etc)
- Malware on mobile device

Weakness
- Mobile applications frequently do not protect network traffic, they may use TLS during authentication, but not elsewhere. In this way, sessionID can be intercepted.
- Poor SSL setup can also facilitate phishing and MITM attack.

Prevention:
- Assume network layer can be eavesdropped
- Apply SSL/TLS to transmit sensitive information, session tokens, or other sensitive backend API
- Account for outside entities like third-party analytics companies, social networks, etc by using their SSL version when an application runs a routine via the browser/webkit. Avoid mixed SSL sessions as they may expose the user's session ID.
- Use strong, industry standard cipher suites with appropriate key length.
- Use certificate signed by trusted CA
- Never allow self-signed certificates, and consider certificate pinning.
- Always require SSL chain verification
- Only establish a secure connection after verifying the identity of the endpoint server using trusted  certificates in the key chain.
- Alert user through the UI if invalid certificate is detected
- Do not send sensitive information over alternate channels (SMS, MMS, or notifications)
- If possible apply separate layer of encryption to any sensitive data before it is given to the SSL channel (in the event that future vulnerabilities in the SSL, there will be a secondary defense)
- Adversary can eavesdrop on sensitive traffic by intercepting the traffic within the mobile device just before the SSL library encrypts and transmits the network traffic.

Android best practices
- Remove all code after the development cycle that may allow the application to accept all certificates such as org.apache.http.conn.ssl.AllowAllHostnameVerifier or SSLSocketFactory.ALLOW_ALL_HOSTNAME_VERIFIER. These equivalent to trusting all certificates.
- If using a class which extends SSLSocketFactory, make sure checkServerTrusted method is properly implemented so that server certificate is correctly checked.

Attack scenarios
- Lack of certificate inspection, the mobile app and an endpoint successfully connect and perform TLS handshake. However the mobile app fails to inspect the certificate offered by the server and the mobile app unconditionally accepts any certificate offered to it by the server. The mobile app is susceptible to MITM through TLS proxy.
- Weak handshake negotiation, the mobile app and endpoint successfully connect and negotiate a cipher suite. The client successfully negotiates with the server to use a weak cipher suite that results in weak encryption that can be easily decrpyted.
- Privacy information leakage, the mobile app transmits PII over non-secure channel instead of SSL.

## M4: Insecure Authentication
Usually using automated attacks that use available or custom-built tools.

Weakness: 
- encourages short passwords/PINs (authentication for mobile apps can be different to web authentication due to availability requirements)
- Mobile apps users not expected to be online at all times during the session (it has uptime requirements to do offline authentication), this offline requirement is something to consider.
- Tester can perform binary attacks against the mobile app while in offline mode, try to bypass offline authentication and try to execute backend server functionality by removing session tokens from POST/GET requests.

Vulnerability:
- Mobile app is able to execute backend API services requests without providing an access token.
- Mobile app stores sensitive data locally on the device
- Uses weak password policy to simplify entering password
- Uses feature like TouchID

