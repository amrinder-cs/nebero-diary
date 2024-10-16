# 13th September

## Daily Log - 13th September

### Changes Made:
- Added `netifyd.zip` to the repository.
- Created a `requiredlibs` script to automate the installation of dependencies and setup for Netify.

### Details:
- **Dependencies Installation**:
    - Installed strict requirements: `libpcap-dev`, `libcurl4-openssl-dev`, `libnetfilter-conntrack-dev`, `libtcmalloc-minimal4`.
    - Installed additional tools: `zlib1g-dev`, `libmnl-dev`, `google-perftools`, `libgoogle-perftools-dev`, `dh-autoreconf`, `make`, `g++`, `curl`, `wget`, `fzf`.

- **Netify Source Download**:
    - Fetched and listed available Netify versions.
    - Used `fzf` for interactive version selection.
    - Downloaded and extracted the selected version.

- **Build and Installation**:
    - Ran `autoupdate` and `./autogen.sh` for preconfiguration.
    - Configured with `./configure --prefix=/opt/netify-agent/ --exec-prefix=/opt/netify-agent/`.
    - Compiled using `make clean` and `make`.
    - Installed using `make install`.

### Script:
```bash
#!/bin/bash
echo "Updating package list before installing locales"
#sudo apt update
#sudo apt install locales

echo "Setting up required locales"
#sudo locale-gen en_US.UTF-8
#sudo dpkg-reconfigure locales

echo "Installing Dependencies"
sudo apt install -y libpcap-dev libcurl4-openssl-dev zlib1g-dev libnetfilter-conntrack-dev libmnl-dev google-perftools libgoogle-perftools-dev libtcmalloc-minimal4 dh-autoreconf make g++ curl wget fzf

echo "Downloading netifyd source"
html_output=$(curl -s "https://download.netify.ai/source/")
version_links=$(echo "$html_output" | grep -oP 'href="netifyd-\d+\.\d+\.\d+\.tar\.gz"' | sed -E 's/href="(netifyd-[^"]+)"/\1/')
reversed_version_links=$(echo "$version_links" | tac)
selected_version=$(echo "$reversed_version_links" | fzf --prompt="Select a version: ")

if [ -z "$selected_version" ]; then
  echo "No version selected. Exiting."
  exit 1
fi

base_url="https://download.netify.ai/source/"
full_url="${base_url}${selected_version}"
wget "$full_url" -O "$selected_version"
tar -xvzf "$selected_version"
dir_name=$(echo "$selected_version" | sed 's/.tar.gz//')
cd "$dir_name" || { echo "Failed to change directory to $dir_name"; exit 1; }

echo "Preconfiguring before make"
autoupdate
./autogen.sh

echo "Configuring"
./configure --prefix=/opt/netify-agent/ --exec-prefix=/opt/netify-agent/

echo "Compiling netifyd agent using make"
make clean
make

echo "Installing"
make install
```