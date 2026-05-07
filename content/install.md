---
title: "Install"
date: 2026-05-07
draft: false
ShowToc: true
TocOpen: true
---

Pre-built packages are published for:

| Family              | Versions                          | Architectures           |
| ------------------- | --------------------------------- | ----------------------- |
| Debian              | 13 (Trixie)                       | amd64, arm64            |
| Ubuntu              | 24.04 LTS (Noble), 25.04 (Plucky) | amd64, arm64            |
| Linux Mint          | 22.x                              | amd64, arm64            |
| Fedora              | 43, 44                            | x86_64, aarch64         |
| RHEL / Rocky / Alma | 9, 10                             | x86_64, aarch64         |
| openSUSE            | Leap 16.0                         | x86_64, aarch64         |
| Arch Linux          | rolling                           | x86_64, aarch64\*       |
| macOS               | moderatly recent                  | x86_64\*\*, aarch64\*\* |

- \* Use the source version.
- \*\* Will use prebuilt binary for aarch64 (apple silicon) and automatically build from source for x86_64 (intel).

## Debian / Ubuntu / Linux Mint

```bash
sudo install -d /etc/apt/keyrings
. /etc/os-release && \
    CODENAME="${UBUNTU_CODENAME:-$VERSION_CODENAME}" && \
    echo "deb [arch=amd64,arm64 signed-by=/etc/apt/keyrings/lolcatpp.asc] https://lolcatpp.github.io/apt $CODENAME main" \
    | sudo tee /etc/apt/sources.list.d/lolcatpp.list

curl -fsSL https://lolcatpp.github.io/apt/pubkey.gpg | sudo tee /etc/apt/keyrings/lolcatpp.asc > /dev/null

sudo apt update
sudo apt install lolcat++
```

Repository: [github.com/lolcatpp/apt](https://github.com/lolcatpp/apt)

## Fedora / RHEL / Rocky / Alma

```bash
. /etc/os-release
case "$ID" in
  fedora)               family="fedora-${VERSION_ID}" ;;
  rhel|rocky|almalinux) family="rhel-${VERSION_ID%%.*}" ;;
  *) echo "unsupported distro: $ID"; exit 1 ;;
esac
sudo curl -fsSLo /etc/yum.repos.d/lolcatpp.repo "https://lolcatpp.github.io/rpm/${family}/lolcatpp.repo"
sudo dnf install -y lolcat++
```

## openSUSE Leap

```bash
. /etc/os-release
sudo zypper addrepo --gpgcheck \
  "https://lolcatpp.github.io/rpm/opensuse-leap-${VERSION_ID}/lolcatpp.repo"
sudo rpm --import https://lolcatpp.github.io/rpm/pubkey.gpg
sudo zypper install lolcat++
```

Repository: [github.com/lolcatpp/rpm](https://github.com/lolcatpp/rpm)

## Arch Linux (AUR)

```bash
# source build
yay -S lolcat++

# pre-built binary
yay -S lolcat++-bin
```

## macOS (Homebrew)

```bash
brew install lolcatpp/tap/lolcatpp
```

## Windows

Download the latest `lolcat-windows-amd64.exe` from the [Releases page](https://github.com/lolcatpp/lolcatpp/releases/latest) and place it somewhere on your `PATH`.

## After installing

`lolcat --help` prints the full set of options:

<picture>
  <source srcset="/help-dark.jpg" media="(prefers-color-scheme: dark)">
  <img src="/help-light.jpg" alt="lolcat++ --help output">
</picture>

## Building from source

```bash
git clone https://github.com/lolcatpp/lolcatpp
cd lolcatpp
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build --parallel
sudo cmake --install build
```

Requires CMake 3.26+, a C++20 compiler, and Boost.ProgramOptions. See the [README](https://github.com/lolcatpp/lolcatpp#building) for full details.
