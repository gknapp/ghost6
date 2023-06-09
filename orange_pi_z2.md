# Orange Pi Zero 2

I bought this SBC to run [klipper](https://www.klipper3d.org) on my [3D Printer](readme.md).

My SBC came with Debian Bullseye pre-installed on a 32GB SDHC as it came as a [kit from TriangleLabs](https://www.aliexpress.com/item/1005004177544221.html).
I connected this board to my network via ethernet and it is automatically provisioned an IP via DHCP.

## Connecting over SSH

Once power and ethernet are connected, you can find the Orange Pi Z2's IP address from your router. When you have this you can login using the credentials:

Username: `root`  
Password: `orangepi`

```bash
ssh root@ip.from.router
```

After pressing [Enter] you'll be prompted for the password.

## Find local update servers (sources.list)

When I received my board, the repositories were set to Chinese servers local to the supplier. I checked the [Debian mirror list](https://www.debian.org/mirror/list) to find a local mirror.

> Note the supported architectures when selecting a mirror, must include 
`arm64`.

When you've selected a local mirror server, note the hostname.

```bash
vim /etc/apt/sources.list
```

Enter:

`:%s/ftp.hk.debian.org/host.you.selected/`

This will replace the hostnames with your chosen one.

> You may need to find a different server for `debian-security` packages.

To save changes and exit vim:

`:x`

> If you made a mistake, or don't want to save your changes, use `:q!`

## Update system packages

```bash
apt update && apt upgrade
```

## Add a new user

It's good practice not to login as `root`, instead we should create a less privileged account with the ability to elevate it's privileges temporarily via the `sudo` command.

```bash
adduser pi && passwd pi
usermod -aG sudo pi
```

## Change the hostname

My Orange Pi Zero 2 was delivered with the hostname: `orangepizero2`

We can change that to something shorter or more memorable. As I'm using this to run klipper on my 3D printer, I thought I'd use the inspired name of `klipper`.

You can change it via one of two ways:

1) Use `orangepi-config` (recommended)
2) Bash commands

Option one:

```bash
orangepi-config
```

Select `Personal`, then the option to change the hostname.

Option two, use bash:

```bash
echo "klipper" > /etc/hostname
hostnamectl set-hostname klipper
```

Then update your `hosts` file to match:

```bash
sed -e 's/orangepizero2/klipper/' -i /etc/hosts
```

## Make connecting easier

Rather than remembering an IP address (that may change) to SSH into, we can make it easier for ourselves with a `.local` domain. This is done via mDNS (multi-cast DNS).

This is easier than it might sound, just install a package called Avahi, an open-source mDNS service:

```bash
apt update
apt install avahi-daemon
```

## Reduce memory usage

We can save memory by not loading unused services and programs. As we're working on the command line using SSH, we can stop the GUI / Window manager from being loaded on boot:

```bash
systemctl set-default multi-user.target
reboot
```

In approximately 30 seconds, you can reconnect via SSH using:

```bash
ssh pi@klipper.local
```

> When you log back in, you'll need to prefix system commands with `sudo`

## Prevent SSH logins as 'root'

Now you have a working user, there's little reason to allow `root` to SSH into your OPi. Especially as the password is known.

```bash
sudo sed -e '/PermitRootLogin/ s/^#*/#/' -i /etc/ssh/sshd_config
```

Restart the SSH service for config changes to take effect.

```bash
sudo systemctl restart ssh
```

## Memory usage

You can see the available memory using the command:

```bash
free
```

## Reduce memory usage: Disable Bluetooth

If you're not going to use Bluetooth you can save memory by disabling the software support using `orangepi-config`, run it and select `Network`:

```bash
sudo orangepi-config
```

## Reduce memory usage: Disable WiFi

If you want to further reduce memory usage, you can disable `wpa_supplicant` via systemd and turn off `wlan0` in Network Manager.

```bash
sudo systemctl stop wpa_supplicant
sudo systemctl disable wpa_supplicant && sudo systemctl mask wpa_supplicant
sudo nmcli radio wifi off
```

I hope this information proved useful.