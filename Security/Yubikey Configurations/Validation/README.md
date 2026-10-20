# Validation

Confirm that the YubiKey is configured as expected after completing the other labs.

[Back to Yubikey Configurations](../README.md)

## References

- [YubiKey Manager CLI User Guide](https://docs.yubico.com/software/yubikey/tools/ykman/)

---

## Validation Checklist

After configuration, run the following commands. Run them as Administrator so that `ykman fido info` works on Windows.

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
- FIDO2 is enabled and configured as expected, with a FIDO2 PIN set.
- PIV is enabled and configured as expected.
- The PIV retry values match the selected security policy.

> Do not post terminal output containing serial numbers, certificate details, usernames, or organization-specific information in public GitHub issues, tickets, or documentation.
