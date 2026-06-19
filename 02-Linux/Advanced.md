# Advanced Linux Operations & System Management

## 🔐 1. SSH (Secure Shell) & Remote Access
* **SSH (Secure Shell)** operates on **PORT 22** and is a protocol (set of rules) that allows one machine to securely connect to another at the shell level.
* It uses **key-based authentication**, making it more secure and difficult to crack via hash values.
* **The Key Pair:** SSH utilizes two keys (a pair).
    * **Private Key:** Stored locally on the source machine (Server a).
    * **Public Key:** Stored on the destination/cloud instance (Server b, e.g., EC2).
* *Analogy:* Think of the local machine as "Ram ji", the destination server as "Sita ji" (Lanka), and the private key/ring carried by "Hanuman ji" connecting them.
* **Connecting to an EC2 Instance:** You can connect via browser-based client, Session Manager, SSH Client, or EC2 serial console.
    * To connect via SSH client: Download the `.pem` file -> Open terminal/GitBash -> Change permissions with `chmod 400 <pem-file.pem>` -> Connect using `ssh -i <pem-file.pem> ubuntu@<public-dns/public IP>`.
* **Key Storage & Management:**
    * SSH keys are created and stored in the `.ssh` folder.
    * The `authorized_keys` file holds the public keys.
    * SSH key configuration files are stored in `/etc/ssh/sshd_config`.
    * The `ssh-keygen` command is used to generate (both keys), manage, and convert auth keys for SSH protocols.
* **Bastion Host:** Also known as a "Jump Server" or "Jump Box", this is a special type of server placed in a public subnet or DMZ that provides a secure entry point for DevOps engineers to access private/internal production servers.

## 📦 2. Package Management
* **Package Installers:** Used to install packages (like Nginx or Docker) in the Linux OS.
    * **Ubuntu:** Uses `apt` (Advanced Package Tool).
    * **CentOS:** Uses `yum`.
    * **RedHat (RHEL):** Uses `rpm` and `dnf`.
* **`apt update` vs `apt upgrade`:**
    * `sudo apt update`: Fetches the latest package information/versions from all configured sources.
    * `sudo apt upgrade`: Actually installs the available upgrades for all currently installed packages.
    * `sudo apt install`: Used for fresh installations.

## 👤 3. User & Group Management
* **Identifying Users:**
    * `whoami`: Shows which user you are currently logged in as.
    * Users include normal users (like `ubuntu`), and `sudo` refers to `root` [admin].
    * `su <user>`: Switches from one user to another.
* **Important Configuration Files:**
    * `/etc/passwd`: Stores user information.
    * `/etc/shadow`: Stores encrypted passwords for users.
    * `/etc/group`: Contains information about multiple users in a group, allowing for bulk permissions.
    * `/etc/gshadow`: Stores encrypted passwords and secure info for groups.
    * `/etc/sudoers`: File used to restrict or define `sudo` permissions.
* **User Commands:** Use `useradd` (creates a user or updates default info), `userdel`, and `passwd` (changes password).
    * *Example:* `sudo useradd -m berlin` adds a new user and creates their home directory. `sudo passwd berlin` sets their password.
    * To specify a shell during creation: Use `which bash` to find the path (e.g., `/usr/bin/bash`), then run `sudo useradd -m tokyo -s /usr/bin/bash`.
* **Group Commands:** `groupadd`, `gpasswd` (administers `/etc/group` and `/etc/gshadow`), and `usermod` (modifies user accounts and system files).
    * *Example:* `sudo groupadd devops` creates a group, and `sudo gpasswd -a tokyo devops` adds user "tokyo" to it.
    * **Docker Group Example:** If `docker ps` gives a "permission denied" error, don't use `sudo` every time. Instead, append the user to the docker group without removing existing memberships using `sudo usermod -aG docker ubuntu`. Run `newgrp docker` to refresh policies.

## 📂 4. File Management, Permissions & Ownership
* **Basic Actions:** Read using `cat`, write using `vim` or `nano`, and execute a shell/executable file using `./`.
* **File Ownership:** If a user cannot write to a file even though permissions look correct, the issue is likely File Ownership.
    * `chown`: Changes the file owner and group. Example: `sudo chown tokyo demo-file.txt`.
    * `chgrp`: Changes *only* the group ownership, not the owner. Example: `sudo chgrp docker hello.txt`.
* **Understanding Permissions:** Linux permissions use a "Triplet" string indicating `directory/file` type, `owner` permissions, `group` permissions, and `other users` permissions.
    * Example string: `d rwx rwx r-x` means it is a directory (`d`) where the owner has read/write/execute (`rwx`), the group has `rwx`, and others have read/execute (`r-x`).
* **Numeric (Binary) Permissions:** Read `r` = 4, Write `w` = 2, Execute `x` = 1.
    * Permissions map to binary where 0 is False and 1 is True (e.g., 4 is 100, 5 is 101, 7 is 111).
    * *Calculation Example:* `664` means 4+2+0 (Owner Read/Write), 4+2+0 (Group Read/Write), 4+0+0 (Others Read).
    * Use the `chmod` command to apply these, e.g., `chmod 400`, `chmod 777`, `chmod 444`.

## ⚙️ 5. Process & Volume Management
* **Process Management:** `systemd` is the first process and handles other processes.
    * You manage services (units) using `systemctl (start | stop | status)`.
    * Logs can be viewed using `journalctl` (e.g., `journalctl -u nginx`).
* **Volume Management:**
    * `lsblk`: Lists all block devices attached to the Linux system. If a new disk is attached to an EC2 instance but isn't visible, check it using `lsblk`.
    * `/etc/fstab`: The file system table. It is used to indirectly configure and permanently mount a volume across reboots.

## 📚 6. Essential DevOps Terminology
* **Fork vs. Clone:**
    * **Clone:** Makes a local copy of a remote repository on your local machine, typically used for teamwork.
    * **Fork:** Creates your own copy of someone else's repository under your GitHub account, typically used for open-source contributions.
* **Runbook:** A short, repeatable checklist followed during an incident. It details the exact command to run, what to observe, and the next action plan if the issue persists.
