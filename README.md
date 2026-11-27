# archinstall-tui-rs

Rust port of [kerembsd/archinstall_tui](https://github.com/kerembsd/archinstall_tui), transpiled deterministically from Bash via [kerembsd/bash2rust](https://github.com/kerembsd/bash2rust) and verified on an Arch Linux live-ISO VM.

## Features

- Interactive `dialog` TUI (`Configuration Hub` and guided setup):
  - Target disk discovery and partitioning (`ext4`, `xfs`, or `btrfs` with subvolumes)
  - Optional LUKS2 full-disk encryption
  - Bootloader (`systemd-boot` / `grub`) and kernel (`linux`, `linux-lts`, `linux-zen`, `linux-hardened`) selection
  - User account, hostname, password strength validation, and login shell (`bash`, `zsh`, `fish`)
  - Locale, keyboard layout, and timezone configuration
  - Desktop environment, display manager, GPU driver, audio stack, network manager, swap, firewall, AUR helper, and optional extras
- `SIGINT` / `EXIT` cleanup traps (`on_interrupt`, `on_exit`)
- Non-destructive `--dry-run` validation mode (default multi-profile checks and custom `DRY_*` environment overrides)

## Requirements

- `dialog` (or `whiptail`) for interactive TUI menus
- Arch Linux live-ISO utilities (`pacstrap`, `genfstab`, `arch-chroot`, `lsblk`, `sgdisk`, `wipefs`, `partprobe`, `udevadm`, `blockdev`, `blkid`, `cryptsetup`, `timedatectl`, `mount`, `umount`, `mountpoint`)

> Note: Run live installations only inside a virtual machine or on a dedicated target machine. Interactive disk partitioning erases the selected target device.

## Build & Usage

Build the release binary:

```bash
cargo build --release
```

Run non-destructive dry-run checks:

```bash
./target/release/archinstall-tui-rs --dry-run
```

Launch the interactive installer TUI:

```bash
./target/release/archinstall-tui-rs
```

## Project Origin

`src/main.rs` is generated deterministically from [kerembsd/archinstall_tui](https://github.com/kerembsd/archinstall_tui) using [kerembsd/bash2rust](https://github.com/kerembsd/bash2rust):

```bash
(cd /path/to/archinstall_tui && bash2rust --file script.sh --migrate /tmp/archinstall_tui_rs_clean)
```

## License

MIT License. See [LICENSE](LICENSE).
