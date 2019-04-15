## Electronic Skill Credential Specification 

## Documentation

1. **[Skill credential vocabulary](v1/context.json)**: JSON-LD context document describing the vocabulary used for credential documents.
1. **[Object model](v1/spec.md#object-model)**: Useful reference for understanding details of properties contained within a credential
1. **[Data model](v1/spec.md#data-model)**: Some helpful notes on modeling credentials data and creating strong identifiers for entities involved in issuing skill credentials.
1. **[Signing](v1/spec.md#appendix-1-signing-procedure-for-assertions-and-evidence) and [Verification guide](v1/spec.md#appendix-3-verifying-authenticity-of-a-certificate)**: Collection of details connected with signing and verification of credential objects

## Utilities 
Cross-language signing and verification libraries are available in Python and JavaScript.

### Python
There is an implementation of credential signing and verification available in [skillcreds-py](https://github.com/project-sunbird/inCredible-py)

Using this library, one can sign a credential in a short snippet of code:

```py
from skillcreds import signatures, suites

key_id = 'https://example.com/keys/exampleKey'
private_key, _ = load_key_pair(key_file)

signature = signatures.LinkedDataSignature(suites.RsaSignature2018())
signed_credential = signature.sign(credential, private_key, key_id)
```  

### JavaScript
There is an implementation of credential signing and verification available in [skillcredjs](https://github.com/project-sunbird/inCredible-js)

Using this library, one can sign a credential using the following snippet:

```js
var sc = require('skillcreds');

var keyId = 'https://example.com/keys/exampleKey';
var privateKey = loadKeyPair(keyFile);
var signature = sc.signatures.LinkedDataSignature(sc.suites.RsaSignature2018());
var signedCredential = signature.sign(credential, privateKey, keyId);
```

## Specification documents

Read the latest specification [here](/v1/spec.md)

