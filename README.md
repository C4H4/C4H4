# C4H4

Coin for H4

# Overview

C4H4 is a centralized coin for H4 project based on [UTXO](https://en.wikipedia.org/wiki/Unspent_transaction_output) and [git](https://en.wikipedia.org/wiki/Git). Voting and multi-signature may be used to decentralize the power of the verifiers, but it is still a kind of centralized implement of digital asset. Although it is a centralized way, all the data is auditable.

The total supply of [C4H4](https://github.com/C4H4/C4H4) is `1` but the coin has infinite divisibility.

Send your transaction by pull request. The transaction is finished once the commit is merged to `master` branch.

Current unspent coins will be placed in `coin` folder. See [Coin](#coin)

# Specification

## Address

Currently we support the following types of address

- RSA

The following types of address will be supported in the future

- ECDSA
- Schnorr
- BLS

### RSA Address Generate

Use the following command to generate a private key of `4096` bits

```sh
openssl genrsa -out key.pem 4096
```

Use the following command to output the public key.

```
openssl rsa -in key.pem -outform PEM -pubout -out key.pub.pem
```

The a `PEM` formatted `4096` bits `RSA` address is generated

```pem
-----BEGIN PUBLIC KEY-----
MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEA50c54B4zoVgFvwUwUu0L
VWSP9z8fDjRYozV/BvaXL+FdffhiIwtvLioe4Iyk9sGtF2HEaQhK/01fEvTMtAeR
JTrB3dlYNGY/JduqmgGvUnEWOMnWsehOWLuYDPgEuvFPgazA606LdCu0qAT2qJJT
46zWpBUeTENQKtWDBM8j89lzNQJmrWPeqbjAauSEt2rjhEa+ZpU/EGz31xKmiMkf
537+nf+YFsgdT+ALshGQZIYG0lFCqWp/y2eIc2/HCUzDDXAWvY5BRS3gpj474x/i
17Ze5515sPtLx7aIuCN0of4AHTH1cOif9k4LuF5CyzKRS5aaZHXt1OMrKcaQft4Y
AgX8bYGDNArD4RSL9KKr12Ly7Pfz2R+ZBClte0nL9Xc4ZttqtIgdw4fCBPQwQOPF
k8L0pamGf6Z3kSPp+MFEo/EfbPOnj+CjrkW3InUKqICoefMUuoQ+1J5HkHu6NtU3
XvepBZoQs60HmHjBXUW03dTi8RTTvJ6Qrdgod92tYCPlrm67LVSoUWS8wuU+5rPh
oQNuDrczfG0XG2opA5Xxdo/OlhwzuRfeb3a4aVtyNJVYQFgo/AEcF4CuhJospV6P
sWucBfdPVYfpvTzxEmduJs/kfVZa7Y1cAX4Ipp2Z5pCgH26cEne1ljDsIKHd9+kg
9ZNEdO0OmrG8KjIQUK1lW6cCAwEAAQ==
-----END PUBLIC KEY-----
```

## Coin

Current unspent coins will be placed in `coin` folder. Each file represents one unspent coin.

### Filename

Filename must be the `SHA-512` digest of its content.

The following command can be used to calculate the digest.

```sh
openssl dgst -sha512 -
```

### Content

The file is in [XML](https://en.wikipedia.org/wiki/XML) format which follows the [DTD](https://en.wikipedia.org/wiki/Document_type_definition) file `c4h4.dtd` in `coin` folder.

```dtd
<!ELEMENT h4 (coin, key)>
<!ELEMENT coin (numerator, denominator)>
<!ELEMENT numerator (#PCDATA)>
<!ELEMENT denominator (#PCDATA)>
<!ELEMENT key (#PCDATA)>
<!ATTLIST key type CDATA #REQUIRED>
<!ATTLIST key format CDATA #REQUIRED>
```
