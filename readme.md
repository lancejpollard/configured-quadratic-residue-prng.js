
# Configured Quadratic Residue PRNG

This builds on top of the general [Quadratic Residue PRNG](https://github.com/lancejpollard/quadratic-residue-prng.js), by selecting perfect prime numbers at various sizes so you can generate seemingly random BigInts at various sizes without having to find and configure the primes yourself.

The bigints are of the order `max = 256 ^ (size / 4)`, where `size` is equal to the left number, and the `max` is on the right:

```
256:  13407807929942597099574024998205846127479365820592393377723561443721764030073546976801874298166903427690031858186486050853753882811946569946433649006084096
128:  115792089237316195423570985008687907853269984665640564039457584007913129639936
96:   6277101735386680763835789423207666416102355444464034512896
64:   340282366920938463463374607431768211456
36:   4722366482869645213696
32:   18446744073709552000
28:   72057594037927940
24:   281474976710656
20:   1099511627776
16:   4294967296
12:   16777216
8:    65536
4:    256
```

Then for each of these, a `p = 3 mod 4` prime was chosen which was just shy of the max, and another prime chosen which was roughly little more than visibly half of the size of the first prime for each size.

You simply take select a number `j` which is fixed during sequence iteration, which ideally is large near the max, say 80-95% of the max. Then you increment `i` and plug it into the question to get a pseudo-random (non-secure) number!

```js
const permute = require('@lancejpollard/configured-quadratic-residue-prng.js')

const size = 16
const j = 42949672
let i = 0n
while (i < j) {
  console.log(permute(i, j, size))
}
```
