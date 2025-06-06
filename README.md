# Fun with Windsor

[Windsor](https://windsorcli.github.io/v0.6.1) is a wonderful project! This repo reflects the fun I have been having with it - and I hope you will too.

On my Macbook Air M1 (RAM 8Gb, SSD 256Gb) with UTM, I create QEMU 7.2 Virtual Machine:

- Name: `wx`,
- Size: 192Gb,
- Network Mode: Bridged (Advanced),
- QEMU: Use local time for base clock,
- Image: ubuntu-24.04.2-live-server-arm64.iso

and add the following line to my `/etc/hosts` (your IP and username will differ):

```
192.168.0.193   wx      # alik
```

Having SSHed to alik@wx, I run there

```
echo 'alik ALL=(ALL) NOPASSWD:ALL' | sudo tee /etc/sudoers.d/alik
exit
```

and complete the setup with

```
bin/uh-setup alik wx windsor-quick-start
```

## Just Read The Instruction

I SSH to `wx` as `root` and proceed with Windsor installation:

```
curl -L -o windsor_0.6.1_linux_arm64.tar.gz https://github.com/windsorcli/cli/releases/download/v0.6.1/windsor_0.6.1_linux_arm64.tar.gz && \
tar -xzf windsor_0.6.1_linux_arm64.tar.gz -C /usr/local/bin && \
chmod +x /usr/local/bin/windsor
...
windsor up --install
```
