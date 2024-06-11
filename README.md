# secrt

Simple wrapper around `systemd-creds` to encrypt user files using the
TPM2.

Files encrypted in that way cannot be open in a different machine, as
it will use the storage root key present in the TPM2 to encrypt the
file.


## Example of use

To encrypt an existent file we can use the `-e` parameter.  This will
generate a new document with `.secrt` extension and will remove the
original one.  To keep the clean file use the `-k` parameter.

```bash
secrt -h

Usage: secrt [OPTION]... [FILE]
Create and edit files encrypted by TPM2

  -h                show this help
  -s                show if dependencies are present
  -k                keep the clean file
  -f                overwrite the encrypted file
  -e  <FILE>        encrypt file and replace it with the new one
  -d  <FILE>        decrypt file to stdout
 [-x] <FILE>        (default) edit encrypted file with $EDITOR (vi)
```

```bash
secrt -e existent-doc
```

To inspect the content of an encrypted file, use the `-d` parameter.
This is like a `cat` operation without a pager.

```bash
secrt -d existent-doc.secrt | less
```

But most of the time we want to edit encrypted files, existent or not.
This command will open an editor (by default `vi`, but can be changed
via the `$EDITOR` environment variable) to change the content of an
encrypted file.

```bash
secrt my-doc.secrt
```

If the file does not exists, a new empty one will be created.
