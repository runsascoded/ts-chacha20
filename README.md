# JS-ChaCha20
Pure JavaScript ChaCha20 stream cipher

### Abstract
ChaCha20 is a stream cipher designed by D. J. Bernstein. 
It is a refinement of the Salsa20 algorithm, and it uses a 256-bit key.

ChaCha20 successively calls the ChaCha20 block function, with the same key and nonce, and with successively increasing block counter parameters.
ChaCha20 then serializes the resulting state by writing the numbers in little-endian order, creating a keystream block.

Concatenating the keystream blocks from the successive blocks forms a keystream.  
The ChaCha20 function then performs an XOR of this keystream with the plaintext.
Alternatively, each keystream block can be XORed with a plaintext block before proceeding to create the next block, saving some memory.
There is no requirement for the plaintext to be an integral multiple of 512 bits.  If there is extra keystream from the last block, it is discarded.

The inputs to ChaCha20 are:
- 256-bit key
- 96-bit nonce.  In some protocols, this is known as the Initialization Vector
- 32-bit initial counter
- Arbitrary-length plaintext

Implementation derived from chacha-ref.c version 20080118
See for details: http://cr.yp.to/chacha/chacha-20080128.pdf

### Install
```
npm install js-chacha20 --save
```

### Usage
Encrypt message with key and nonce
```javascript
import JSChaCha20 from "js-chacha20";

const key = Uint8Array([...]); // 32 bytes key
const nonce = Uint8Array([...]); // 12 bytes nonce
const message = Uint8Array([...]); // some data as bytes array

// Encrypt //
const encrypt = new JSChaCha20(key, nonce).encrypt(message);

// now encrypt contains bytes array of encrypted message
```

Decrypt encrypted message with key and nonce
```javascript
import JSChaCha20 from "js-chacha20";

const key = Uint8Array([...]); // 32 bytes key
const nonce = Uint8Array([...]); // 12 bytes nonce
const encrypt = Uint8Array([...]); // some data as bytes array

// Encrypt //
const message = new JSChaCha20(key, nonce).decrypt(encrypt);

// now message contains bytes array of original message
```

That all. If something happens, Error will be thrown.
More examples you can find in tests files.
