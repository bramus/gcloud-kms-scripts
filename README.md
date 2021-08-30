# Google Cloud Platform KMS encryption utilities

A collection of scripts here to help interact with [Google's Cloud Key Management Service](https://cloud.google.com/kms/), without too many layers of indirection.

## The utilities

  * `kms-encrypt` - Encrypt a plaintext string to a secret
  * `kms-decrypt` - Decrypt a secret to a plaintext string

Each script can be invoked with `-h` to see it's usage.

## Examples

### Encrypt


```bash
kms-encrypt -r "projects/[PROJECT_ID]/locations/[LOCATION]/keyRings/[keyring_name]/cryptoKeys/[key_name]"
```

`kms-encrypt` will ask for a plaintext string to encrypt and yield the encrypted result:

```
Please enter a plaintext string to encrypt
> test
CiQAUqQA4o9w4O3ovBCcj…
```

Alternatively, you can pass plaintext string to encrypt into `kms-encrypt`:

```bash
kms-encrypt -r "projects/[PROJECT_ID]/locations/[LOCATION]/keyRings/[keyring_name]/cryptoKeys/[key_name]" -p test
# "CiQAUqQA4o9w4O3ovBCcj…"
```

```bash
echo -n test | kms-encrypt -r "projects/[PROJECT_ID]/locations/[LOCATION]/keyRings/[keyring_name]/cryptoKeys/[key_name]"
# "CiQAUqQA4o9w4O3ovBCcj…"
```

### Decrypt

```bash
kms-decrypt -r "projects/[PROJECT_ID]/locations/[LOCATION]/keyRings/[keyring_name]/cryptoKeys/[key_name]"
```

`kms-decrypt` will ask for a secret to decrypt and yield the plaintext result:

```
Please enter a secret to decrypt
> CiQAUqQA4o9w4O3ovBCcj…
test
```

Alternatively, you can pass secret to decrypt into `kms-decrypt`:

```bash
kms-decrypt -r "projects/[PROJECT_ID]/locations/[LOCATION]/keyRings/[keyring_name]/cryptoKeys/[key_name]" -s "CiQAUqQA4o9w4O3ovBCcj…"
# test
```

```bash
echo -n "CiQAUqQA4o9w4O3ovBCcj…" | kms-decrypt -r "projects/[PROJECT_ID]/locations/[LOCATION]/keyRings/[keyring_name]/cryptoKeys/[key_name]"
# test
```

## License

`glcoud-kms-scripts` is released under the MIT License. See the enclosed [`LICENSE` file](LICENSE) for details.

## Acknowledgements

This code is inspired upon the [KMS encryption utilities for AWS by James Gregory](https://github.com/jagregory/kms-scripts/)