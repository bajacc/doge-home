# Doge Home

A 100% secure smart home writen in rust for the raspberry pi

## Emulate the raspberi pi 1

Dockerpi emulate a raspberypi in a docker using qemu

```bash
sudo docker run -it -p 5022:5022 -v $HOME/.dockerpi:/sdcard lukechilds/dockerpi
```

It will create an image for the raspberry pi and launch this image.
ssh is not active by default. in order to activate ssh, login into the raspberry pi:

```bash
login: pi
password: raspberry
```

Go to `/etc/ssh/sshd_config` and uncomment the following lines:

```bash
#Port 22
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::
```

then

```bash
systemctl enable ssh
systemctl start ssh
```

This way you can connect to your emulated raspberrypi:

```bash
ssh -p 5022 pi@localhost
```

## cross compiling rust for the raspberry pi

Raspberrypi 0/1 use arm and 2/3 use armv7. In order to compile your code from your x86/x64 machine, you need to use specific tools.
Cross compilation is done using cross:
<https://github.com/rust-embedded/cross>

To install cross, execute:
```bash 
cargo install cross
```

The `deploy.sh` script compile, deploy, and execute the binary on the targeted raspberry pi. You must add your user to the docker group in order to compile with cross. If ssh does not work, check if you dockerpi is running.