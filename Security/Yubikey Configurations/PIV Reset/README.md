# PIV Reset

Return the YubiKey's PIV (smart card) application to factory settings. Use this when both the PIV PIN and PUK are blocked, or when the key is being reissued.

[Back to Yubikey Configurations](../README.md)

## References

- [PIV Commands](https://docs.yubico.com/software/yubikey/tools/ykman/PIV_Commands.html)

> **Warning:** A PIV reset wipes all PIV data on the YubiKey, including private keys and certificates, and restores the PIV PIN, PUK, and management key to factory defaults. Anything that depends on those certificates, such as smart-card sign-in, signing, or SSH, stops working until new keys and certificates are created.
>
> The PIV reset does **not** affect the FIDO2 application. FIDO2 passkeys and the FIDO2 PIN remain unchanged.

---

## Reset the PIV Application

1. Open **Command Prompt** or **PowerShell**.

2. Review the current PIV status:

```powershell
ykman piv info
```

3. Run the reset command:

```powershell
ykman piv reset
```

4. Type `y` to confirm the warning when prompted.

5. Verify the reset:

```powershell
ykman piv info
```

Confirm that no certificates are listed and the PIN and PUK retry counts are back to their defaults.

> `ykman piv reset` is not available in `ykman` version 5.4.0. Update `ykman` using the [CLI Setup](../CLI%20Setup/README.md) lab if the command is missing.

---

## Factory Defaults After Reset

| Item | Default value |
|---|---|
| PIV PIN | `123456` |
| PUK | `12345678` |
| Management key | `010203040506070801020304050607080102030405060708` |

These defaults are publicly known. Change all three right away.

---

Next: [PIV Retry Limits](../PIV%20Retry%20Limits/README.md)
