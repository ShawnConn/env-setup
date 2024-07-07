# env-setup test vm scripts
This directory contains files & scripts to test env-setup on a Tart VM when 
using _Apple Silicon_.

## test scripts
The `scripts` directory has a few scripts to test the running VM:

- [scripts/create-tart-vms](scripts/create-tart-vms): create a 20GB ubuntu & 60GB macos VM.
- [scripts/env-setup](scripts/env-setup): test the [env-setup script](../scripts/env-setup).
- [scripts/init-test](scripts/init-test): test the [init script](../scripts/init).
- [scripts/scp](scripts/ssh): scp file/dir into the VM.
- [scripts/ssh](scripts/ssh): ssh into the VM.

### linux
See the [Tart quickstart guide](https://tart.run/quick-start/#vm-images) for how to start up a linux VM.
```
# Create a 20GB ubuntu & 60GB macos VMs:
./scripts/create-tart-vms 
tart run ubuntu

# in another shell while `tart run` is running...
# test the init script that's hosted on https://example.com/env-setup
./scripts/init-test https://example.com/env-setup

# run/setup env-setup with an interactive prompt for the playbook
./scripts/env-setup 

# run 01-config env-setup playbook
./scripts/env-setup 01-config

# copy config.yml to VM
./scripts/scp config.yml /Users/admin/env-setup/config.yml

# SSH into VM
./scripts/ssh
```

### macos
See the [Tart quickstart guide](https://tart.run/quick-start/#vm-images) for how to start up a macos VM.

```
# Create a 20GB ubuntu & 60GB macos VMs:
./scripts/create-tart-vms 
tart run sonoma-vanilla

# in another shell while `tart run` is running...
# test the init script that's hosted on https://example.com/env-setup
./scripts/init-test https://example.com/env-setup

# run/setup env-setup with an interactive prompt for the playbook
./scripts/env-setup 

# run 01-config env-setup playbook
./scripts/env-setup 01-config

# copy config.yml to VM
./scripts/scp config.yml /Users/admin/env-setup/config.yml

# SSH into VM
./scripts/ssh
```

# Prerequisites
- A mac running on Apple Silicon
- The `tart` && `sshpass` tools installed (`brew install cirruslabs/cli/tart && brew install cirruslabs/cli/sshpass`)

# Notes

