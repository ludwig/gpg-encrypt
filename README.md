# gpg-encrypt:<br>encrypt a file using our best settings

Syntax:

    gpg-encrypt <file>

Example:

    $ gpg-encrypt example.txt

Output is a new encrypted file:

    example.txt.gpg

To decrypt the file:

    gpg -d example.txt.gpg

Also see our `gpg-decrypt` command to decrypt a file using our best settings.

## Settings

  * Symmetric encryption, i.e. we use the same password for encryption and decryption.
    We choose this because our users can understand symmetric more easily than asymmetic.

  * Encryption using the aes256 cipher algorithm.
    We choose this because it's a good balance of strong, fast, and portable.

  * Digesting using the sha256 digest algorithm.
    We choose this because it's a good balance of strong, fast, and portable.

  * No compression, because typically our files are small or already compressed.
    We choose this to maximize portability, PGP compatibility, and speed.

  * Explicit settings, rather than depending on defaults.

  * Suitable for GPG v2; backwards-compatible with GPG v1 when possible.

## Command

The command is:

    gpg --symmetric \
    --cipher-algo aes256 \
    --digest-algo sha256 \
    --cert-digest-algo sha256 \
    --compress-algo none -z 0 \
    --quiet --no-greeting \
    "$@"

## Older versions

If you use GPG v1, and you want to skip the GPG user agent, then you may want to add this option:

    --no-use-agent


## Alternatives

Here's an alternative to wrapping GPG, using .gnupg/gpg.conf:

    personal-cipher-preferences AES256 AES
    personal-digest-preferences SHA256 SHA512
    personal-compress-preferences Uncompressed
    default-preference-list SHA256 SHA512 AES256 AES Uncompressed

    cert-digest-algo SHA256

    s2k-cipher-algo AES256
    s2k-digest-algo SHA256
    s2k-mode 3
    s2k-count 65011712

    disable-cipher-algo 3DES
    weak-digest SHA1
    force-mdc

Note that these options impact compatibility with other GPG/PGP clients.

Credit: User twr at https://news.ycombinator.com/item?id=13382734
