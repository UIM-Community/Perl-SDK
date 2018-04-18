# Encryption API

This API will let you encrypt and decrypt string key. A complete example is available [here](https://github.com/UIM-Community/Perl-SDK/blob/master/examples/encrypt-cfg-file.md).

## API

### nimEncryptString(szKey, szString) -> String

Will encrypt the input string using the Twofish algorithm and the encryption key. The function returns a base64
encoded and encrypted string. The result must be freed after use.

### nimDecryptString(szKey, szCrypted) -> String

The input string must be encrypted by nimEncryptString and the key must be the same. The result must be freed
after use.
