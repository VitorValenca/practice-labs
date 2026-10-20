# PIV Retry Limits

Set how many incorrect PIV PIN and PUK attempts are allowed before each one is blocked. PIV supports smart-card capabilities, including certificate-based authentication, digital signatures, and some SSH or Windows sign-in configurations.

[Back to Yubikey Configurations](../README.md)

## References

- [PIV Commands](https://docs.yubico.com/software/yubikey/tools/ykman/PIV_Commands.html)

> **Important:** Run this lab before changing the PIV PIN or PUK. Setting retry values resets the PIV PIN and PUK to factory defaults.

---

## Configure PIV Retry Limits

1. Choose the desired retry limits:

- `PIN-RETRIES`: Number of incorrect PIV PIN attempts allowed before the PIN is blocked.
- `PUK-RETRIES`: Number of incorrect PUK attempts allowed before the PUK is blocked.

2. Run the command, replacing the placeholders with your desired values:

```powershell
ykman piv access set-retries <PIN-RETRIES> <PUK-RETRIES>
```

Example: Set five PIV PIN attempts and five PUK attempts:

```powershell
ykman piv access set-retries 5 5
```

3. Confirm the change when prompted.

> After setting retries, the PIV PIN and PUK return to their factory defaults. Change both immediately.

---

Next: [PIV PIN and PUK](../PIV%20PIN%20and%20PUK/README.md)
