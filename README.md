# ExCrypto.NET
Extends .NET Crypto API with support for symmetric ciphers ChaCha and Salsa and their variants.

Features:
- Partially vectorized code, optimized for x86/x64 (SSE 128bit, AVX-256 256bit)(Xor operations)
- Efficient memory access
- Integrated into .NET Crypto API, compatible with existing API
- Unit tests provided
- Tested against all the test vectors provided on the: https://tools.ietf.org/html/rfc7539
- 

ToDo:
- vectorize rest of the code once Microsoft releases required vector instructions
- possibly vectorize poly1305 while code access remains in constant-time (against side-channel attacks)
