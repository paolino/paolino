# Get my 1Password Secret Key from a hardware key

For the day every device is gone. You need: the hardware key and its PIN, an internet connection, and your 1Password account password (from memory).

**Linux / macOS** (terminal):

    curl -fsSL https://raw.githubusercontent.com/paolino/paolino/main/recover/recover.sh | sh

**Windows** (Terminal or PowerShell *as Administrator*):

    irm https://raw.githubusercontent.com/paolino/paolino/main/recover/recover.ps1 | iex

Enter the PIN, touch the key. The Secret Key is copied to the clipboard (cleared after 60 s). Then sign in at https://my.1password.com with your email, the Secret Key (paste) and your password.

A page that shows the same commands: https://lambdasistemi.net/recover/

## What it does

Downloads `age` and `age-plugin-fido2-hmac`, checks them against sha256 checksums pinned in the script, fetches the public bundle in this repository (`recovery.age`, `recovery.ids`), decrypts it with the key, prints nothing secret, and deletes everything it downloaded.

## What you give up

The Secret Key is stored in a **public** file, locked to hardware keys. Someone holding one of those keys *and* its PIN can read it. They still need your account password to sign in, but the Secret Key then no longer adds its extra protection against someone who gets hold of your password hash from elsewhere. Use a strong account password.

## Tested / not tested

- Tested: Ubuntu 24.04 desktop VM with only public downloads; the key on the clipboard matched the real one and 1Password sign-in worked.
- **Not tested:** Windows (`recover.ps1`), macOS.
- The plugin has one maintainer and upstream publishes no checksums, so the pinned ones are trust-on-first-use.
