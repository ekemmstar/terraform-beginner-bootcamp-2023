# Terraform Beginner Bootcamp 2023
# Semantic Versioning :mage:


This project is going to utilize semantic versioning for its tagging.
[semver.org](https://semver.org/)

The general format: 

**MAJOR.MINOR.PATCH**, `1.0.1`
- **MAJOR**. version when you make incompatible API changes
- **MINOR**. version when you add functionality in a backward compatible manner
- **PATCH**.version when you make backward compatible bug fixes

Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

## Install the Terraform CLI

## Considerations with the Terraform CLI changes

The Terraform CLI installation instruction have changed due to gpg keyring changes. So we needed refer to the latest install CLI instructions via Terraform Documentation and  change the scripting for install.
[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Considerations for Linux Distribution

This project is built against Ubuntu.
please consider checking your Linux Distribution and change according to distribution needs
[How to Check OS Version in Linux](https://www.cyberciti.biz/faq/
https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/)

Example of checking OS Version
```
$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy

```
### Refactoring into Bash Scripts
While fixing the Terraform CLI gpg depreciation issue, we notice that bash scripts steps were a considerable amount of more code. So we decided to create a bash sript to install the Terraform CLI.

This bash script is located here: [./bin/install_terraform_cli](/bin/install_terraform_cli)

- This will keep the Gitpod Task file([.gitpod.yml](.gitpod.yml)) tidy.
- This allow us an easier to debug and execute manually Terraform CLI install
- THIS Will allow better portability for other projects that need to install Terraform CLI


#### Shebang Considerations
A Shabang (pronounced Sha-bang)tells the bash script what program will interpret the script.e.g `#!/bin/bash`

ChatGPT recommend this format for bash: `#!/usr/bin/env bash`
- For portability for different OS distributions
- will search the user´s PATH for the bash execution

https://en.wikipedia.org/wiki/Shebang_(Unix)


#### Execution Consideration
When executing the bash script we can use the `./` shorthand notation to execute the bash script. e.g `./bin/install_terraform_cli`

If we are using a sccript in .gitpod.yml we need to point the script to a program to interpret it e.g `source ./bin/install_terraform_cli`


#### Linux Permissions Consideration

In order to make our bash scripts executable we need to change linux permission for the fix to be executable at the user mode.
```sh
chmod u+x ./bin/install_terraform_cli
```

Alternatively:
```sh
chmod 744 ./bin/install_terraform_cli
```

https://en.wikipedia.org/wiki/Chmod

### Gitpod Lifecycle (Before, Init, Command)

We need to be careful when using the Init because it will not rerun if we restart an existing workspace.

https://www.gitpod.io/docs/configure/workspaces/workspace-lifecycle

