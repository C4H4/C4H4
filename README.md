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

## Transfer

### Create the Transaction

synchronize the repository

```sh
git checkout master
git pull
```

remove old coins

```sh
rm coin/00bf5fcb92bfddb1f41ea9372e6868b9e25466c310f140240c8809710fdb2e0acb525a7f494d5188fb79ba00006770add75a81408cbe914f71449603ee24c785.xml
```

create new coins and name the file as `temp.1.xml`, `temp.2.xml`

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<!DOCTYPE h4 SYSTEM "c4h4.dtd">
<h4>
    <coin>
        <numerator>1</numerator>
        <denominator>2</denominator>
    </coin>
    <key type="rsa" format="pem">
        -----BEGIN PUBLIC KEY-----
        MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAm4VFEKwcbTmMWT1rkubc
        XbzYGscBx+Y+tFqTROKL4SAVLZx4LzcqHFMA7x+FO8A2h1IPiNDcbA/4MAUFsMjn
        6CjG3WafV3Zx4HZSmxcleUIuNYMsTOfProj3Qa9OE4MYOJmPNQy1NG1oeMo1PXzc
        5FcGPeW0EJpBdb7lG7nZSZxmoo2dQVj2NF4S22YaJMWAZa1cXbfxu5WgvJhVxp+R
        PavfhmOz0OpEmqk+jMG2n7c23vMWdsVeg1Mh3RHseEIgF+1+N8Lg+aMQ7KmX2u7f
        eWGGHX11+1UAS/qTjSSVZ2jhB6EG/pPEeLTpgNkdnLWE1F6Mz9/JKvKDRcane9yj
        rMr+PJQSaegfWX76KEHF9mgrRaoQtzhk/ToO7iESGusn7fKdEGQCSN7wqZBvwHVF
        Nuyv5xz6t3C35ntWUF7PH8Grt8LZtYURz4iTScZ4NPsAt7huO9qR0mYAQ5qKkLJD
        JRjERaAD7AyAyQI6uc4QTD7J39grScITCxYw4emoUqa97ENttp9S2R8QyZ6KiN27
        JHB2SmFKV1lzjaEjEjGiLWm+JpFY5gBsK4mYGFweXF+bJk1LvbsK/fQ+2WpVC/LC
        5AO7zbgoH38zzfkpc0PcOokc/fJM0R5kqFuzQuMUAXZmF4lN7/xb2FNDBdVx2vcF
        1tl8dVfMGodhIfpTiidheUcCAwEAAQ==
        -----END PUBLIC KEY-----        
    </key>
</h4>
```

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<!DOCTYPE h4 SYSTEM "c4h4.dtd">
<h4>
    <coin>
        <numerator>1</numerator>
        <denominator>2</denominator>
    </coin>
    <key type="rsa" format="pem">
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
    </key>
</h4>
```

calculate the digest of the new coins and place the new coins to the `coin` folder

```sh
mv temp.1.xml coin/$(openssl dgst -sha512 -r temp.1.xml |cut -d ' ' -f 1).xml
mv temp.2.xml coin/$(openssl dgst -sha512 -r temp.2.xml |cut -d ' ' -f 1).xml
```

### Sign the Transaction

git add the change

```sh
git add coin/
```

create `diff.log`

```sh
git diff --name-status --no-renames --cached > diff.log
```

sign `diff.log` by private key `key.pem`

```sh
openssl dgst -sha512 -sign key.pem -out diff.sign diff.log
```

encode `diff.sign` to hex format

```sh
xxd -p diff.sign diff.sign.enc
```

commit the change

```sh
git commit -F diff.sign.enc
```

### Send the Transaction

push the commit and submit pull request

```sh
git push
```

once the pull request is merged to `master` branch, the transaction is finished.

## Verify

```sh
git diff --name-status --no-renames master > diff.log
```

```sh
git log -n 1 --format=%B 5fbc808302409d7870627be58f209aad4ae29e77 > diff.sign.enc
```

```sh
xxd -r -p diff.sign.enc diff.sign
```

```sh
openssl dgst -verify key.pub.pem -sha512 -signature diff.sign diff.log
```

```sh
git log --pretty=format: --name-only --diff-filter=A --no-renames coin
```