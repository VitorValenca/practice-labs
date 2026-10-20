# PIV Management Key

Replace the default PIV management key. The management key protects administrative PIV actions, such as generating key pairs and managing certificates.

[Back to Yubikey Configurations](../README.md)

## References

- [PIV Commands](https://docs.yubico.com/software/yubikey/tools/ykman/PIV_Commands.html)

> **Before you start:** Change the PIV PIN first using the [PIV PIN and PUK](../PIV%20PIN%20and%20PUK/README.md) lab. The command below protects the new management key with the PIV PIN.

---

## Configure the PIV Management Key

The command below:

- Generates a random AES-256 management key.
- Stores the management key on the YubiKey.
- Protects the management key with the PIV PIN.
- Requires physical touch of the YubiKey for management-key operations.

1. Run:

```powershell
ykman piv access change-management-key --algorithm AES256 --generate --protect --touch
```

2. Enter the current management key when prompted.

3. Enter the PIV PIN when prompted.

4. Touch the YubiKey when prompted.

> Do not use a manually selected or shared management key unless required by an approved organizational security policy.

---

Next: [Validation](../Validation/README.md)
