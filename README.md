# ExCrypto.NET
Extends .NET crypto API with support for symmetric ciphers ChaCha and Salsa and their variants

Features:
- Partially vectorized code, optimized for x86/x64 (SSE, AVX)(Xor operations)
- Efficient memory access
-  
-
-

ToDo:
- vectorize rest of the code once Microsoft releases new vector instructions needed
- possibly vectorize poly1305 while code access remains in constant-time (against side-channel attacks)
