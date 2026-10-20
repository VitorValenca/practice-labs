# FIDO2 PIN

Set or change the FIDO2 PIN. The FIDO2 PIN protects passkeys, passwordless sign-in, and supported multi-factor authentication workflows.

[Back to Yubikey Configurations](../README.md)

## References

- [FIDO Commands](https://docs.yubico.com/software/yubikey/tools/ykman/FIDO_Commands.html)
- [YubiKey Technical Manual: FIDO Specifics](https://docs.yubico.com/hardware/yubikey/yk-tech-manual/yk5-apps-fido.html)

---

## PIN Requirements

- The FIDO2 PIN must be at least 4 alphanumeric characters.
- Some YubiKey models or enterprise policies may require a longer PIN.
- YubiKeys ship with no FIDO2 PIN set, and a FIDO2 reset also removes the PIN. Some keys issued through YubiKey as a Service may come with a preset PIN that must be changed on first use.
- `123456` is the default **PIV** PIN, not a FIDO2 PIN.
- Changing the FIDO2 PIN does **not** change the PIV PIN, PUK, or management key.

> Characters do not display while entering a PIN. This is expected behavior.

---

## Set or Change the FIDO2 PIN

1. Open **Command Prompt** or **PowerShell** as Administrator.

> Administrator privileges are required on Windows when running commands that begin with `ykman fido`.

2. Run the following command:

```powershell
ykman fido access change-pin
```

3. If a FIDO2 PIN is already set, enter the current FIDO2 PIN when prompted. If no PIN is set, `ykman` prompts only for the new PIN.

4. Enter the new FIDO2 PIN.

5. Re-enter the new FIDO2 PIN to confirm it.

6. Confirm that the command reports:

```text
FIDO PIN updated.
```

7. Save the new FIDO2 PIN in an approved password manager or credential vault.

8. Optional: Verify the PIN and reset the FIDO2 PIN retry counter:

```powershell
ykman fido access verify-pin
```

> If the command reports `ERROR: Wrong PIN`, verify the current PIN before trying again. Repeated failed attempts can block FIDO2 PIN access. If the PIN is blocked or forgotten, the only recovery is a [FIDO2 Reset](../FIDO2%20Reset/README.md).

---

Next: [PIV Reset](../PIV%20Reset/README.md) or [PIV Retry Limits](../PIV%20Retry%20Limits/README.md)
