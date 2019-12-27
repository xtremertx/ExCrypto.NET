# ExCrypto.NET
Extends .NET Crypto API with support for symmetric ciphers ChaCha and Salsa and their respective variants. Also featuring Poly1305 a secret-key message-authentication code reference implementation. All the algorithms are based on work by Daniel J. Bernstein.

Features:
---------
- **ChaCha** and **Salsa** symmetric ciphers with **256-bit security strength** using 20, 12 or 8 rounds (impl. can handle any amouth of rounds that satisfy the following conditions: N >= 8 and N % 2 == 0, where N = amouth of rounds)
- Both Salsa and Chacha cipher do support **original** and **RFC7539** variant (RFC was customized for network protocol use, originals are better suited for HDD encryption as they can handle more data per (key, nonce) pair, RFC was also specifically for ChaCha).
- Fully optimized code using branches that are specifically crafted for x86/x64 instruction set.
- Partially vectorized code (SIMD), specifically XOR instructions for best performance (supporting: SSE 128bit, AVX-256 256bit)
- Efficient memory access in Poly1305 (reusing of constant-buffer for hash output)
- Integrated into .NET Crypto API, fully compatible with existing API.
- Unit tests provided (encryption, decryption, inner state, reusing instances, etc.)
- Implemented and tested against all the test vectors provided on the: https://tools.ietf.org/html/rfc7539 (see: unit tests section)
- Benchmark rutine provided (i5-4690K 4-cores, no HT, 3.5Ghz; 16GB DDR3 RAM 1600Mhz, Stats: ~ 110MB/s enc, ~ 102MB/s dec)

Usage
-----
- See Wiki

Support Overview
------------------

| Feature | ChaCha | Salsa |
| ------------- | ------------- | ------------- |
| 256-bit key | Yes | Yes |
| 128-bit key | No | No |
| Rounds amouth | 20, 12, 8 | 20, 12, 8 |
| RFC 7539 variant | Yes | Yes(\*) |
| Original paper variant | Yes | Yes |

\**RFC 7539 was originaly intended only for ChaCha, however I have implemented it for Salsa too.* 

Considerations:
---------------
- This implementation tries to offer a minimalistic code, good efficiency and security.
- You may use different implementation in case you need higher performance implementation (MB/s), especially in case of HDD encryption where you are encrypting big files.
- Poly1305 is well tested but does not feature best performance, also its implementation is not using constant-memory access (without allocations) which may or may not be used for side-channel attacks.
- Both Chacha and Salsa do not support 128-bit version.

ToDo:
-----

.NET Core
----------
- [ ] consider .NET Core port (using full **SIMD support with Span and Memory** optimizations and using **Unsafe** class)

.NET Framework
----------------
- [ ] vectorize rest of the code once Microsoft releases required vector instructions
- [ ] add parallel support to use multiple cores?
- [ ] use x64 (long/ulong) to access state of cipher to get ~1-5% speed-up?
- [ ] possibly vectorize poly1305 while code access remains in constant-time (against side-channel attacks) and allocations must use constant-memory not variable-memory as BitInteger impl (security)
