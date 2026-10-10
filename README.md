wget -O /tmp/onedrive-release.key "https://download.opensuse.org/repositories/home:/npreining:/debian-ubuntu-onedrive/Debian_13/Release.key"


gpg --show-keys /tmp/onedrive-release.key



sudo gpg --dearmor --yes --output /usr/share/keyrings/obs-onedrive.gpg /tmp/onedrive-release.key



wget -qO - https://download.opensuse.org/repositories/home:/npreining:/debian-ubuntu-onedrive/Debian_13/Release.key | gpg --dearmor | sudo tee /usr/share/keyrings/obs-onedrive.gpg > /dev/null


echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/obs-onedrive.gpg] https://download.opensuse.org/repositories/home:/npreining:/debian-ubuntu-onedrive/Debian_13/ ./" | sudo tee /etc/apt/sources.list.d/onedrive.list


sudo apt update
sudo apt install --no-install-recommends --no-install-suggests onedrive

onedrive --sync --verbose --dry-run


onedrive --sync --verbose


sudo systemctl enable --now "onedrive@$(whoami).service"


sudo systemctl status "onedrive@$(whoami).service"
