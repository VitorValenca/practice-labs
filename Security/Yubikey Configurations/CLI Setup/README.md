# CLI Setup

Install or update the YubiKey Manager CLI (`ykman`) on Windows and confirm that the YubiKey is detected.

[Back to Yubikey Configurations](../README.md)

## References

- [YubiKey Manager CLI Installation](https://docs.yubico.com/software/yubikey/tools/ykman/Install_ykman.html)
- [YubiKey Manager CLI User Guide](https://docs.yubico.com/software/yubikey/tools/ykman/)

> **Prerequisites:** Python 3.10 or later and `pip` must be installed before using the Python package installation method.

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

---

Next: [FIDO2 Reset](../FIDO2%20Reset/README.md) or [FIDO2 PIN](../FIDO2%20PIN/README.md)
