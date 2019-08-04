# ExCrypto.NET
Extends .NET Crypto API with support for symmetric ciphers ChaCha and Salsa and their respective variants.

Features:
- ChaCha and Salsa with 256-bit security strength using 20, 12 or 8 rounds (but in reality any number N >= 8 and N % 2 == 0 is supported)
- Supports original Salsa/Chacha variant and RFC7539 variant of both ciphers (RFC was customized for network protocol use, originals are better for HDD encryption as they can handle more data).
- Fully optimized code using branches that are specifically crafted for x86/x64 instruction set.
- Partially vectorized code, specifically XOR SIMD vectorization which is using CPU avaible instruction set for best performance (SSE 128bit, AVX-256 256bit - Xor op)
- Efficient memory access (reusing of buffers)
- Integrated into .NET Crypto API, fully compatible with existing API (like it was original algorithm)
- Unit tests provided (encryption, decryption, inner state, reusing, etc.)
- Implemented and tested against all the test vectors provided on the: https://tools.ietf.org/html/rfc7539 (see unit tests)
- Benchmark test provided (i5-4690K 4-cores, no HT, 3.5Ghz; 16GB DDR3 RAM 1600Mhz - 110MB/s enc, 102MB/s dec)

ToDo:
-----

.NET Core
----------
- [ ] consider .NET Core port (using full SIMD support with Span<T> and Memory<T> optimizations and using Unsafe class)

.NET Framework
----------------
- [ ] vectorize rest of the code once Microsoft releases required vector instructions
- [ ] add parallel support to use multiple cores?
- [ ] use x64 (long/ulong) to access state of cipher to get ~1-5% speed-up?
- [ ] possibly vectorize poly1305 while code access remains in constant-time (against side-channel attacks) and allocations must use constant-memory not variable-memory as BitInteger impl (security)
