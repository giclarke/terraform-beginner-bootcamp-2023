# Terraform Beginner Bootcamp 2023

## Semantic Versioning :mage:

This project is going to utilize semantic versioninng for its tagging.
[semver.org](https://semver.org/)

The general format:

**MAJOR.MINOR.PATCH**, eg. `1.0.1`

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes
Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

## Install the Terraform CLI

### Considerations with the Terraform CLI changes
The Terraform CLI installation instructions have changed due to gpg keyring changes. As a result, we utilized the latest install CLI instructions via Terraform Documentation and changed the scripting for install.

[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Considerations for Linux Distribution

This project is built in Ubuntu.
Please check Linux Distribution and change accordingly to your specific distribution needs. 

Check the following sites to determine OS versions:

[How To Check OS Version in Linux](https://www.cyberciti.biz/faq/how-to-check-os-version-in-Linux-command-line)

[How to Find Which Linux Version You Are Running](https://linuxhandbook.com/check-linux-version/)


Example of checking OS Version:
```
$cat /etc/os-release

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

While fixing the Terraform CLI gpg deprecation issues, we noticed that Bash script steps used a considerably amount of code when compaired to the original.  As a result, we decided to create a Bash script to install the Terraform CLI.

This Bach script is located here: [./bin/install_terraform_cli](./bin/install_terraform_cli)

- This will keep the Gitpod Task File less cluttered. ([.gitpod.yml](./gitpod.yml)). 
- This will also allow us to easily debug and  execute Terraform CLI install manually. 
- This will allow better portability for other projects that need to install Terraform CLI.

#### Shebang Considerations

A Shebang (pronounced Sha-bang), tells the Bash script what program it will use to interpret the script - Example `#!/bin/bash`

ChatGPT recommended this format for Bash: `#!/usr/bin/env bash`

- Portability on different OS Distributions
- Searching the user's PATH for the Bash executable

You can find more information at this link: [Shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))

## Execution Considerations

When executing the Bash script, we can use the `./` shortcut notation to execute the Bash script.

Example: `./bin/install_terraform_cli`

If we are using a script in .gitpod.yml, we need to point the script to a program that will interpret it.

Example: `source ./bin/install_terraform_cli`

#### Linux Permissions Considerations

In order to make our Bash scripts executable, we need to change Linux permissions for the fix to be executable at the user mode.

```sh
chmod u+x ./bin/install_terraform_cli
```

Another example:

```sh
chmod 744 ./bin/install_terraform_cli
```

#### The main parts of the chmod permissions:

For example: rwxr-x---

Each group of three characters define permissions for each class:

The three leftmost characters, rwx, define permissions for the **User** class (i.e. the file owner).

The middle three characters, r-x, define permissions for the **Group** class (i.e. the group owning the file).

The rightmost three characters, ---, define permissions for the **Others** class. In this example, users who are not the owner of the file and who are not members of the Group (and, thus, are in the Others class) have no permission to access the file.


Here are additional links to research further:

[Wikipedia's Explanation On chmod](https://en.wikipedia.org/wiki/Chmod)

[How to Change File Permissions and Ownership in Linux](https://www.freecodecamp.org/news/linux-chmod-chown-change-file-permissions/)

[How to Use the chmod Command on Linux](https://www.howtogeek.com/437958/how-to-use-the-chmod-command-on-linux/)

[Linux permissions - An introduction to chmod](https://www.redhat.com/sysadmin/introduction-chmod)

### Github Lifecycle (Before, Init, Command)

**NOTE** - We need to be careful when using **Init** because it will not re-run if we restart an existing workspace.

#### Execution order
With Gitpod, you have the following three types of tasks:

- **before**: Use this for tasks that need to run before init and before command. For example, customize the terminal or install global project dependencies.
- **init**: Use this for heavy-lifting tasks such as downloading dependencies or compiling source code.
- **command**: Use this to start your database or development server.

The order in which these tasks execute depends on whether you have Prebuilds configured for your project and which startup scenario applies. 

Click [here](https://www.gitpod.io/docs/configure/workspaces/tasks) for more information.