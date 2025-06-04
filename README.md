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

Still no luck:

```
root@wx:~/project/windsor-quick-start# windsor init local
✔ 📥 Loading component cluster/talos - Done
✔ 📥 Loading component gitops/flux - Done
Initialization successful
root@wx:~/project/windsor-quick-start# windsor check
✔ 🛠️ Checking tool versions - Done
All tools are up to date.
root@wx:~/project/windsor-quick-start# windsor context get
local
root@wx:~/project/windsor-quick-start# windsor up --install
✔ 📥 Loading component cluster/talos - Done
✔ 📥 Loading component gitops/flux - Done
✔ 📦 Running docker compose up - Done
✔ 🔐 Writing DNS configuration to /etc/systemd/resolved.conf.d/dns-override-test.conf - Done
🔐 Restarting systemd-resolved
✔ 🔐 Restarting systemd-resolved - Done
✔ 🌎 Initializing Terraform in cluster/talos - Done
✔ 🌎 Planning Terraform changes in cluster/talos - Done
✔ 🌎 Applying Terraform changes in cluster/talos - Done
✔ 🌎 Initializing Terraform in gitops/flux - Done
✔ 🌎 Planning Terraform changes in gitops/flux - Done

[ExecProgress ERROR]
Command: terraform [apply]
Stdout:
module.main.kubernetes_namespace.flux_system: Creating...
module.main.kubernetes_namespace.flux_system: Creation complete after 0s [id=system-gitops]
module.main.kubernetes_secret.webhook_token: Creating...
module.main.kubernetes_secret.git_auth: Creating...
module.main.kubernetes_secret.git_auth: Creation complete after 0s [id=system-gitops/flux-system]
module.main.kubernetes_secret.webhook_token: Creation complete after 0s [id=system-gitops/webhook-token]
module.main.helm_release.flux_system: Creating...
module.main.helm_release.flux_system: Still creating... [10s elapsed]
module.main.helm_release.flux_system: Still creating... [20s elapsed]
module.main.helm_release.flux_system: Still creating... [30s elapsed]
module.main.helm_release.flux_system: Still creating... [40s elapsed]
module.main.helm_release.flux_system: Still creating... [50s elapsed]
module.main.helm_release.flux_system: Still creating... [1m0s elapsed]
module.main.helm_release.flux_system: Still creating... [1m10s elapsed]
module.main.helm_release.flux_system: Still creating... [1m20s elapsed]
module.main.helm_release.flux_system: Still creating... [1m30s elapsed]
module.main.helm_release.flux_system: Still creating... [1m40s elapsed]
module.main.helm_release.flux_system: Still creating... [1m50s elapsed]
module.main.helm_release.flux_system: Still creating... [2m0s elapsed]
module.main.helm_release.flux_system: Still creating... [2m10s elapsed]
module.main.helm_release.flux_system: Still creating... [2m20s elapsed]
module.main.helm_release.flux_system: Still creating... [2m30s elapsed]
module.main.helm_release.flux_system: Still creating... [2m40s elapsed]
module.main.helm_release.flux_system: Still creating... [2m50s elapsed]
module.main.helm_release.flux_system: Still creating... [3m0s elapsed]
module.main.helm_release.flux_system: Still creating... [3m10s elapsed]
module.main.helm_release.flux_system: Still creating... [3m20s elapsed]
module.main.helm_release.flux_system: Still creating... [3m30s elapsed]
module.main.helm_release.flux_system: Still creating... [3m40s elapsed]
module.main.helm_release.flux_system: Still creating... [3m50s elapsed]
module.main.helm_release.flux_system: Still creating... [4m0s elapsed]
module.main.helm_release.flux_system: Still creating... [4m10s elapsed]
module.main.helm_release.flux_system: Still creating... [4m20s elapsed]
module.main.helm_release.flux_system: Still creating... [4m30s elapsed]
module.main.helm_release.flux_system: Still creating... [4m40s elapsed]
module.main.helm_release.flux_system: Still creating... [4m50s elapsed]
module.main.helm_release.flux_system: Still creating... [5m0s elapsed]
╷
│ Warning: Helm release "" was created but has a failed status. Use the `helm` command to investigate the error, correct it, then run Terraform again.
│ 
│   with module.main.helm_release.flux_system,
│   on /root/project/windsor-quick-start/contexts/local/.terraform/gitops/flux/modules/main/terraform/gitops/flux/main.tf line 35, in resource "helm_release" "flux_system":
│   35: resource "helm_release" "flux_system" {
│ 
╵

Stderr:
╷
│ Error: failed pre-install: 1 error occurred:
│ 	* timed out waiting for the condition
│ 
│ 
│ 
│   with module.main.helm_release.flux_system,
│   on /root/project/windsor-quick-start/contexts/local/.terraform/gitops/flux/modules/main/terraform/gitops/flux/main.tf line 35, in resource "helm_release" "flux_system":
│   35: resource "helm_release" "flux_system" {
│ 
╵

Error: <nil>
Error: Error running stack Up command: error applying Terraform changes in /root/project/windsor-quick-start/.windsor/.tf_modules/gitops/flux: command execution failed: exit status 1
root@wx:~/project/windsor-quick-start# 
```
