# Yubikey Configurations

Labs for setting up, securing, and resetting a YubiKey on Windows with the YubiKey Manager command-line interface (`ykman`). Each folder covers one function and has its own README.

> **Notice:** The YubiKey Manager GUI reached End of Life on February 19, 2026. These labs use the supported `ykman` command-line interface (CLI).
>
> **Platform:** These instructions are written for Windows.
>
> **Prerequisites:** Python 3.10 or later and `pip` must be installed before using the Python package installation method.

---

## Labs

Complete the labs in this order for a new or freshly reset YubiKey:

| Step | Lab | Purpose |
|---|---|---|
| 1 | [CLI Setup](./CLI%20Setup/README.md) | Install `ykman` and confirm the YubiKey is detected |
| 2 | [FIDO2 Reset](./FIDO2%20Reset/README.md) | Return the FIDO2 application to factory settings (optional) |
| 3 | [FIDO2 PIN](./FIDO2%20PIN/README.md) | Set or change the FIDO2 PIN |
| 4 | [PIV Reset](./PIV%20Reset/README.md) | Return the PIV application to factory settings (optional) |
| 5 | [PIV Retry Limits](./PIV%20Retry%20Limits/README.md) | Set PIV PIN and PUK retry limits |
| 6 | [PIV PIN and PUK](./PIV%20PIN%20and%20PUK/README.md) | Change the PIV PIN and PUK, and unblock a PIN |
| 7 | [PIV Management Key](./PIV%20Management%20Key/README.md) | Replace the default PIV management key |
| 8 | [Validation](./Validation/README.md) | Confirm the final configuration |

> **Order matters for PIV:** Set PIV retry limits **before** changing the PIV PIN or PUK. The retry command resets the PIV PIN and PUK to factory defaults.

---

## Security Notes

- Do not place PINs, PUKs, or management keys directly in commands. Doing so can expose sensitive values through terminal history, logs, or process listings.
- Use an approved password manager or credential vault to securely record new PINs, PUKs, and recovery information.
- FIDO2 and PIV are independent applications. Changing or resetting one does **not** change the other.
- Do not post terminal output containing serial numbers, certificate details, usernames, or organization-specific information in public GitHub issues, tickets, or documentation.

---

## References

- [YubiKey Manager CLI User Guide](https://docs.yubico.com/software/yubikey/tools/ykman/)
- [YubiKey Manager CLI Installation](https://docs.yubico.com/software/yubikey/tools/ykman/Install_ykman.html)
- [FIDO Commands](https://docs.yubico.com/software/yubikey/tools/ykman/FIDO_Commands.html)
- [PIV Commands](https://docs.yubico.com/software/yubikey/tools/ykman/PIV_Commands.html)
- [YubiKey Technical Manual: FIDO Specifics](https://docs.yubico.com/hardware/yubikey/yk-tech-manual/yk5-apps-fido.html)
- [Yubico End-of-Life Products](https://www.yubico.com/support/terms-conditions/yubico-end-of-life-policy/eol-products/)
