# YubiKey Manager CLI: Initial Security Configuration

## References

- [YubiKey Manager CLI User Guide](https://docs.yubico.com/software/yubikey/tools/ykman/)
- [YubiKey Manager CLI Installation](https://docs.yubico.com/software/yubikey/tools/ykman/Install_ykman.html)
- [FIDO Commands](https://docs.yubico.com/software/yubikey/tools/ykman/FIDO_Commands.html)
- [PIV Commands](https://docs.yubico.com/software/yubikey/tools/ykman/PIV_Commands.html)
- [Yubico End-of-Life Products](https://www.yubico.com/support/terms-conditions/yubico-end-of-life-policy/eol-products/)

> **Notice:** The YubiKey Manager GUI reached End of Life on February 19, 2026. This guide uses the supported `ykman` command-line interface (CLI).
>
> **Platform:** These instructions are written for Windows.
>
> **Prerequisites:** Python 3.10 or later and `pip` must be installed before using the Python package installation method.

---

## Security Notes

- Do not place PINs, PUKs, or management keys directly in commands. Doing so can expose sensitive values through terminal history, logs, or process listings.
- Use an approved password manager or credential vault to securely record new PINs, PUKs, and recovery information.
- FIDO2 and PIV are independent applications. Changing a FIDO2 PIN does **not** change the PIV PIN, PUK, or management key.
- Configure PIV retry limits **before** changing the PIV PIN or PUK. The retry configuration command resets the PIV PIN and PUK to factory defaults.

---

## Install or Update YubiKey Manager

1. Open **Command Prompt** or **PowerShell** as Administrator.

> Administrator privileges are required on Windows when running commands that begin with `ykman fido`.

2. Install YubiKey Manager:

```powershell
py -m pip install --user yubikey-manager
```

3. Update an existing installation:

```powershell
py -m pip install --user --upgrade yubikey-manager
```

4. Verify the installation:

```powershell
ykman --version
```

Expected output:

```text
YubiKey Manager (ykman) version: 5.9.2
```

> If `ykman` is not recognized as a command, close and reopen the terminal. If the issue continues, verify that Python's user `Scripts` directory is included in the system `PATH`.

---

## Connect and Verify the YubiKey

1. Insert the YubiKey into an available USB port.

2. Verify that the YubiKey is detected:

```powershell
ykman list
```

3. View general YubiKey information, including firmware, serial number, enabled interfaces, and application status:

```powershell
ykman info
```

4. View FIDO2 configuration information:

```powershell
ykman fido info
```

5. View PIV configuration information:

```powershell
ykman piv info
```

---

## Configure the FIDO2 PIN

The FIDO2 PIN protects passkeys, passwordless sign-in, and supported multi-factor authentication workflows.

- The FIDO2 PIN must be at least 4 alphanumeric characters.
- Some YubiKey models or enterprise policies may require a longer PIN.
- A new YubiKey may use `123456` as the default FIDO2 PIN.

> Characters do not display while entering a PIN. This is expected behavior.

1. Run the following command:

```powershell
ykman fido access change-pin
```

2. Enter the current FIDO2 PIN when prompted.

3. Enter the new FIDO2 PIN.

4. Re-enter the new FIDO2 PIN to confirm it.

5. Confirm that the command reports:

```text
FIDO PIN updated.
```

6. Optional: Verify the PIN and reset the FIDO2 PIN retry counter:

```powershell
ykman fido access verify-pin
```

> If the command reports `ERROR: Wrong PIN`, verify the current PIN before trying again. Repeated failed attempts can block FIDO2 PIN access.

---

## Configure PIV Retry Limits

PIV supports smart-card capabilities, including certificate-based authentication, digital signatures, and some SSH or Windows sign-in configurations.

> **Important:** Run this step before changing the PIV PIN or PUK. Setting retry values resets the PIV PIN and PUK to factory defaults.

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

### Unblock a PIV PIN

If the PIV PIN becomes blocked, use the PUK to create a new PIV PIN:

```powershell
ykman piv access unblock-pin
```

Enter the PUK when prompted, then enter and confirm a new PIV PIN.

> If the PUK becomes blocked, it cannot be used to recover the PIV application.

---

## Configure the PIV Management Key

The PIV management key protects administrative PIV actions, such as generating key pairs and managing certificates.

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

## Validation Checklist

After configuration, run the following commands:

```powershell
ykman info
```

```powershell
ykman fido info
```

```powershell
ykman piv info
```

Confirm that:

- The YubiKey is detected.
- FIDO2 is enabled and configured as expected.
- PIV is enabled and configured as expected.
- The PIV retry values match the selected security policy.

> Do not post terminal output containing serial numbers, certificate details, usernames, or organization-specific information in public GitHub issues, tickets, or documentation.

---

## Helpful Commands

Display general help:

```powershell
ykman --help
```

Display FIDO2 command help:

```powershell
ykman fido --help
```

Display PIV access command help:

```powershell
ykman piv access --help
```
