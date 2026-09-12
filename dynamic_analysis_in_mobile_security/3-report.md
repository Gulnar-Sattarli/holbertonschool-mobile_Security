Objective

The objective was to identify hidden flag-processing methods within Apk_task3.apk, initialize the required class at runtime, and invoke the discovered methods dynamically to recover the concealed flag.

Key Findings
Target Class: com.example.app.SecretUtils
Identified Methods: decryptFlag(String) and decodeBase64Custom(String)
Recovered Flag: FLAG{h1dd3n_m3thod_inv0k3d_3xp0s3d_2026}
Methodology

1. Static Analysis
The APK was decompiled using jadx to examine the application's classes and methods. During the analysis, com.example.app.SecretUtils was identified as containing flag-processing functionality that was not directly exposed through the application's normal execution flow.

2. Runtime Class Initialization
Frida was used to access the Java runtime and create an instance of the SecretUtils class. The Java.use() API was used to obtain the class wrapper, while $new() was used to initialize the required object within the application process.

3. Hidden Method Invocation
The decryptFlag() method was invoked dynamically with the required input. Its output produced an intermediate encoded value, which was then supplied to decodeBase64Custom() for further processing.

4. Decoding & Flag Recovery
The custom decoding routine was analyzed to reverse the Base64 transformation and byte-level XOR obfuscation. After applying the decoding process, the original plaintext flag was successfully recovered.

Result

The hidden functionality was successfully invoked at runtime, and the concealed flag was extracted:

FLAG{h1dd3n_m3thod_inv0k3d_3xp0s3d_2026}
