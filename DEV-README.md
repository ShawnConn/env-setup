# Development
This repo is designed to be forked/extended/reused to fit a user or 
organization's environment setup needs.

If you want to create your own variant, you can fork this repo, and then alter 
the `scripts/init` and `*.yml` config files to point your own repo URLs.

## Design
There isn't much to env-setup. To use one sentence, it's a text user interface 
for Git, Ansible, & Homebrew to install/configure your macos / Linux 
environment.

If you want to do development, see the summary/notes on each of its 
components below. 

### Ansible Playbooks
The `ansible` [directory](ansible) contains all the playbooks that will run in either the 
macOS / Linux environment. Both sets of playbooks re-use the same manifest 
variables in `*.yml` but run the task in different ways. For example, Homebrew's 
[Cask system](https://github.com/Homebrew/homebrew-cask) for app delivery 
doesn't work in a Linux environment, so a variable map attempts to find the 
closest app that might be available for the package manager.

Most playbooks share the same config file symlinked from the `.00-init` 
playbook so they only need to be edited once.

The `.00-init` playbook is designed to be an initial startup playbook that 
should only run once (a `.init` file is placed here as marker to note this). 
All other playbooks can be ran multiple times as needed by user.

### Router
The `router` [directory](router) is a [Hono](https://hono.dev/) URL router that delivers 
a init bash script when `https://example.com/env-setup` is requested in a 
`curl` command. 

The router uses TypeScript/Hono and can be tested locally with Cloudflare 
[Wranger](https://developers.cloudflare.com/workers/wrangler/) and run live 
with [Workers](https://developers.cloudflare.com/workers/). It assumes this 
repo is hosted on GitHub so alterative Git hosting might will need changes.

It's a bit overengineered, but it enables possible dyanmic script generation 
in the future. 

This is an optional component for script delivery; nothing prevents you from 
placing a static script on a web server as an alternative here to delivery the 
[init script](scripts/init).

### Scripts
The `scripts` [directory](scripts) is the "front end" here. Everything is written in bash 
and will work in either a macOS / Linux environment. The scripts are mostly 
logic to confirm Git is setup (to deliver `env-setup`) and Ansible is ready to 
run. After thatt, the user can then select their config & Ansible playbook 
to run when needed.

If you need to troubleshoot issues with `env-setup`, running `env-setup -v` will
run the bash scripting & Ansible playbook with the verbose flag. If you need 
to do further debugging with the playbook tasks, refer to the Ansible 
docs on [debugging playbooks](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_debugger.html).

## Testing
The `terraform` [directory](terraform) is a basic Terraform module that will stand up a SSH 
key and Linux (Ubuntu 20) & macOS (Ventura) EC2 VMs. 

Once built, there are a few [scripts](terraform/scripts) that can be used to 
test running `env-setup` in a new environment.
