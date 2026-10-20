# PIV PIN and PUK

Change the PIV PIN and PUK, and use the PUK to unblock a blocked PIV PIN.

[Back to Yubikey Configurations](../README.md)

## References

- [PIV Commands](https://docs.yubico.com/software/yubikey/tools/ykman/PIV_Commands.html)

> **Before you start:** If you plan to change PIV retry limits, complete the [PIV Retry Limits](../PIV%20Retry%20Limits/README.md) lab first. Setting retries resets the PIV PIN and PUK to factory defaults.

---

## Configure the PIV PIN

The PIV PIN authorizes smart-card operations, such as using certificates for authentication or signing.

- The PIV PIN must be between 6 and 8 alphanumeric characters.
- Numeric-only PINs are recommended for cross-platform compatibility.
- The factory-default PIV PIN is typically `123456`.

1. Run:

```powershell
ykman piv access change-pin
```

2. Enter the current PIV PIN when prompted.

3. Enter a new PIV PIN.

4. Re-enter the new PIV PIN to confirm it.

5. Save the new PIV PIN in an approved password manager or credential vault.

---

## Configure the PIV PUK

The PUK, or PIN Unblocking Key, is used to unblock the PIV PIN after too many failed PIN attempts.

- The PUK is separate from the PIV PIN.
- The PUK must be between 6 and 8 alphanumeric characters.
- The factory-default PUK is typically `12345678`.

1. Run:

```powershell
ykman piv access change-puk
```

2. Enter the current PUK when prompted.

3. Enter a new PUK.

4. Re-enter the new PUK to confirm it.

5. Store the new PUK securely, preferably separately from the YubiKey.

---

## Unblock a PIV PIN

If the PIV PIN becomes blocked, use the PUK to create a new PIV PIN:

```powershell
ykman piv access unblock-pin
```

Enter the PUK when prompted, then enter and confirm a new PIV PIN.

> If the PUK becomes blocked, it cannot be used to recover the PIV application. The only recovery is a [PIV Reset](../PIV%20Reset/README.md), which deletes all PIV keys and certificates.

---

Next: [PIV Management Key](../PIV%20Management%20Key/README.md)
