## Electronic Skill Credential Specification 

### Documentation

You may be interested in reading the latest [specification](/v1/spec.pdf) or the accompanying [implementation guide](/v1/implementation_guide.pdf)


### References

1. **Object model**: you may find details of the specification's [object model](object-model) a useful reference
1. **Data model**: here are some helpful notes on [modeling credentials data](data-model) and creating strong identifiers for entities involved in issuing skill credentials.

### Utilities 
Cross-language signing and verification libraries are available in Python and JavaScript.

#### Python
There is an implementation of credential signing and verification available in [skillcreds-py](https://github.com/bharatskills/skillcreds-py)

Using this library, one can sign a credential in a short snippet of code:

```py
from skillcreds import signatures, suites

key_id = 'https://example.com/keys/exampleKey'
private_key, _ = load_key_pair(key_file)

signature = signatures.LinkedDataSignature(suites.RsaSignature2018())
signed_credential = signature.sign(credential, private_key, key_id)
```  

#### JavaScript
There is an implementation of credential signing and verification available in [skillcredjs](https://github.com/bharatskills/skillcredsjs)

Using this library, one can sign a credential using the following snippet:

```js
var sc = require('skillcreds');

var keyId = 'https://example.com/keys/exampleKey';
var privateKey = loadKeyPair(keyFile);
var signature = sc.signatures.LinkedDataSignature(sc.suites.RsaSignature2018());
var signedCredential = signature.sign(credential, privateKey, keyId);
```
