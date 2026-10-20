# FIDO2 Reset

Return the YubiKey's FIDO2 application to factory settings. Use this when the FIDO2 PIN is forgotten or blocked, or when the key is being reissued.

[Back to Yubikey Configurations](../README.md)

## References

- [FIDO Commands](https://docs.yubico.com/software/yubikey/tools/ykman/FIDO_Commands.html)
- [YubiKey Technical Manual: FIDO Specifics](https://docs.yubico.com/hardware/yubikey/yk-tech-manual/yk5-apps-fido.html)

> **Warning:** A reset permanently deletes all FIDO credentials on the YubiKey, including passkeys and FIDO U2F credentials, and removes the FIDO2 PIN. Accounts that use this key for sign-in will no longer accept it until it is registered again. Confirm that each affected account has a backup sign-in method or a backup security key before continuing.
>
> The FIDO2 reset does **not** affect the PIV application. The PIV PIN, PUK, management key, and certificates remain unchanged.

---

## Reset the FIDO2 Application

1. Open **Command Prompt** or **PowerShell** as Administrator.

> Administrator privileges are required on Windows when running commands that begin with `ykman fido`.

2. Review the current FIDO2 status:

```powershell
ykman fido info
```

3. Run the reset command:

```powershell
ykman fido reset
```

4. Type `y` to confirm the warning when prompted.

5. If prompted, remove and reinsert the YubiKey. The reset must happen right after the YubiKey is inserted.

6. Touch the YubiKey when it blinks to complete the reset.

7. Verify the reset:

```powershell
ykman fido info
```

Confirm that the output shows no FIDO2 PIN is set.

> If the reset fails because too much time passed after inserting the YubiKey, run `ykman fido reset` again and touch the key promptly after reinserting it.

---

Next: [FIDO2 PIN](../FIDO2%20PIN/README.md). Set a new FIDO2 PIN before using the YubiKey again.
