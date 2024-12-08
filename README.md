# bitlocked-ntfs-manger
A simple Bash utility for securely managing and mounting BitLocker-encrypted portable SSDs on Linux. Stores PSSD credentials encrypted with GPG, lets you add device info, unlock and mount drives, and cleanly unmount them with a menu-driven interface.

## Improvement Checklist for the bitlocked-ntfs-manger Script

### Password Security
- [ ] Avoid using `--passphrase` on the command line for GPG operations.
- [ ] Implement secure password input for GPG (e.g., using `--pinentry-mode` or a password pipe).
- [ ] Scrub sensitive data (e.g., `PASSWORD`, `MEMORY_PASSWORD`) from memory after use.

### Device Detection and Mounting
- [ ] Prompt the user to confirm detected device and partition before proceeding.
- [ ] Add stricter checks to verify the selected device matches the intended PSSD.
- [ ] Handle scenarios where multiple USB devices are connected gracefully.

### Encryption Practices
- [ ] Enforce strong password requirements for `MEMORY_PASSWORD`.
- [ ] Set strict file permissions (e.g., `chmod 600 ~/.pssd_memory.gpg`) for the encrypted memory file.
- [ ] Use GPG's stronger defaults for symmetric encryption if possible.

### Temporary Files
- [ ] Store temporary files (e.g., `/tmp/dislocker.log`) in a secure directory, such as `/run/user/$UID`.
- [ ] Delete temporary files immediately after use.

### Input Validation
- [ ] Validate USB ID input to match the format `0000:0000`.
- [ ] Sanitize nickname inputs to disallow unsafe characters.
- [ ] Reject empty or malformed inputs for passwords and other fields.

### Error Handling
- [ ] Provide detailed error messages for mounting, decryption, and other critical operations.
- [ ] Maintain a secure (encrypted) error log for debugging.
- [ ] Implement fallback mechanisms if `dislocker` or mounting fails.

### Privilege Escalation
- [ ] Check if the user has `sudo` privileges before running privileged commands.
- [ ] Request `sudo` only when necessary for specific commands (e.g., `mount`, `umount`).
- [ ] Add error handling for failed `sudo` commands.

### Modularity
- [ ] Refactor the script to use smaller, modular functions for readability and maintainability.
- [ ] Separate concerns such as input handling, device detection, and encryption into individual modules.

### User Interface
- [ ] Implement a more user-friendly interface using tools like `dialog` or `whiptail`.
- [ ] Add clear instructions or a help menu to guide the user through the script.

### Documentation
- [ ] Update the README to include usage instructions and security best practices.
- [ ] Document changes and provide examples for secure password management.
- [ ] Add a troubleshooting section for common issues and their resolutions.

### Testing
- [ ] Test the script with multiple USB devices connected to ensure proper detection.
- [ ] Test error handling scenarios (e.g., invalid inputs, missing dependencies, and failed commands).
- [ ] Validate the security of encrypted files and memory handling.

### Optional Enhancements
- [ ] Add support for additional encryption mechanisms beyond GPG.
- [ ] Provide an option to manage multiple user profiles for PSSD credentials.
- [ ] Implement logging with rotation and encryption for detailed activity tracking.
