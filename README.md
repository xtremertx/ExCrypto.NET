# ExCrypto.NET
Extends .NET Crypto API with support for symmetric ciphers ChaCha and Salsa and their respective variants.

Features:
- ChaCha and Salsa with 256-bit security strength using 20, 12 or 8 rounds (but in reality any number > 8 is supported)
- Partially vectorized code, optimized for x86/x64 (SSE 128bit, AVX-256 256bit)(Xor operations)
- Efficient memory access
- Integrated into .NET Crypto API, compatible with existing API
- Unit tests provided
- Tested against all the test vectors provided on the: https://tools.ietf.org/html/rfc7539
- 

ToDo:
- consider .NET Core port (using full SIMD support with Span<T> and Memory<T> optimizations and using Unsafe class)
- vectorize rest of the code once Microsoft releases required vector instructions
- add parallel support to use multiple cores
- use x64 (long/ulong) to access state of cipher to get ~1-5% speed-up?
- possibly vectorize poly1305 while code access remains in constant-time (against side-channel attacks) and allocations must use constant-memory not variable-memory as BitInteger impl (security)
