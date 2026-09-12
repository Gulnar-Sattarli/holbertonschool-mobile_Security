Objective

The goal was to intercept the encrypted HTTPS communication of Apk_task2.apk, bypass the application's SSL pinning mechanism, identify the cryptographic parameters used to protect the server response, and recover the flag through offline decryption.

Key Findings
Analysis Tools: Burp Suite Community, Frida, Objection
SSL Pinning Bypass: Runtime instrumentation using Frida/Objection
Encryption Algorithm: AES/CBC/PKCS5Padding
Encryption Key: 321c_s3cr3t_k3y!
Initialization Vector: 1234567890abcdef
Recovered Flag: FLAG{a3s_cbc_n3tw0rk_d3cryp110n_succ3ss_2026}
Methodology

1. HTTPS Traffic Interception
Burp Suite was configured as a proxy, and its CA certificate was installed on the test device. Since the application implemented SSL pinning, Objection was used to disable the relevant certificate-pinning mechanisms at runtime.

2. Application Analysis
The APK was decompiled with jadx-gui to examine the application's network and cryptographic logic. The response-processing functionality was traced to com.example.cryptoapp.network.CryptoManager.

3. Cryptographic Parameter Identification
Analysis of the decompiled code revealed hardcoded AES parameters, including the encryption key and initialization vector used for processing the server response.

4. Payload Decryption
The intercepted server response was Base64-decoded and then decrypted offline using AES in CBC mode with PKCS5 padding and the identified key/IV pair.

5. Result
The decryption process successfully recovered the plaintext flag:

FLAG{a3s_cbc_n3tw0rk_d3cryp110n_succ3ss_2026}
