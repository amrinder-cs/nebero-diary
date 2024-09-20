# 11th September

### Summary:
A shell script was crafted to automate the installation of dependencies, setting up locales, downloading, extracting, configuring, compiling, and installing the Netify agent from source.

### Elaborate Steps:

1. **Installing Dependencies:**
    - Installed various development libraries and tools required for building the Netify agent using `sudo apt install`. These include libraries for pcap, curl, zlib, netfilter, mnl, Google performance tools, and other build tools like `make`, `g++`, `curl`, `wget`, and `fzf`.

     ```shell
     sudo apt install -y libpcap-dev libcurl4-openssl-dev zlib1g-dev libnetfilter-conntrack-dev libmnl-dev google-perftools libgoogle-perftools-dev libtcmalloc-minimal4 dh-autoreconf make g++ curl wget fzf
     ```

2. **Setting Up Locales:**
    - Generated and configured the `en_US.UTF-8` locale, which is required for Netify.

     ```shell
     sudo locale-gen en_US.UTF-8
     sudo dpkg-reconfigure locales
     ```

3. **Downloading Netify Source:**
    - Fetched the HTML output from the Netify source download page and extracted links to `.tar.gz` files.
    - reversed the list of versions and used `fzf` to select a version interactively.
    - constructed the full URL for the selected version and downloaded it using `wget`.
    - extracted the downloaded `.tar.gz` file and changed the directory to the extracted directory.

     ```shell
     html_output=$(curl -s "https://download.netify.ai/source/")
     version_links=$(echo "$html_output" | grep -oP 'href="netifyd-\d+\.\d+\.\d+\.tar\.gz"' | sed -E 's/href="(netifyd-[^"]+)"/\1/')
     reversed_version_links=$(echo "$version_links" | tac)
     selected_version=$(echo "$reversed_version_links" | fzf --prompt="Select a version: ")
     base_url="https://download.netify.ai/source/"
     full_url="${base_url}${selected_version}"
     wget "$full_url" -O "$selected_version"
     tar -xvzf "$selected_version"
     dir_name=$(echo "$selected_version" | sed 's/.tar.gz//')
     cd "$dir_name" || { echo "Failed to change directory to $dir_name"; exit 1; }
     ```

4. **Preconfiguring and Configuring:**
    - ran `autoupdate` and `./autogen.sh` to prepare the build system.
    - configured the build system using `./configure`.

     ```shell
     autoupdate
     ./autogen.sh
     ./configure
     ```

5. **Compiling and Installing:**
    - Cleaned any previous builds using `make clean`.
    - Compiled the Netify agent using `make`.
    - Finally, installed the compiled Netify agent using `make install`.

     ```shell
     make clean
     make
     make install
     ```

These steps collectively automate the process of setting up the environment, downloading, building, and installing the Netify agent from source.

