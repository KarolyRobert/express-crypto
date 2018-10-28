# roger-express-crypto

A roger-express-crypto egy express middleware, privát weboldalak ajax forgalmának titkosítására.
A forgalom titkosítása 256-bites AES kulccsal történik amit a cliens előzőleg generált RSA kulcsok segítségével szerezhet meg.

## installáció:

`npm i roger-express-crypto`

## Használat:

### RSA kulcsok generálása:

Az projekt `package.json -> scripts` szekciójában fel kell venni a kulcsok generálására szolgáló segédprogramot.

```
"scripts" : {
    "keygen" : "roger-express-crypto"
}
```

Futtatás pl:
`npm run keygen keys 2048`
Ezzel a parancsal létrejön a projekt gyökér könyvtárában egy keys könyvtár ahol a kulcsok ezután megtalálhatók lesznek.

### A middleware.

```javascript
const express = require("express");
const crypto = require("roger-express-crypto");

const app = express();

var myCrypto = new crypto({
  serverkey: "A server titkos RSA kulcsa",
  clientkey: "A cliens nyilvános RSA kulcsa"
});

app.use(myCrypto.middleware);
```
