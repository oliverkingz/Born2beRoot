# Born2BeRoot   
[42 CUrsus] Born2BeRoot is a project focused on setting up and configuring a virtual machine (VM) with strict security and system administration rules. The goal is to create a secure and efficient server environment using Debian, with features like SSH, UFW firewall, sudo configurations, and a custom monitoring script. Additionally, the project includes bonus features such as setting up WordPress with Lighttpd, MariaDB, and PHP, as well as adding an additional service like LiteSpeed for enhanced performance.

Keywords  
- **Virtual Machine**
- **Debian**
- **SSH**
- **UFW**
- **Sudo**
- **LVM**
- **WordPress**
- **MariaDB**
- **PHP**
- **LiteSpeed**

---

## Index

- [Overview](#overview)
- [Features](#features)
- [Bonus Features](#bonus-features)
- [Requirements](#requirements)
- [How to Run](#how-to-run)
  - [Example Usage](#example-usage)
  - [Bonus Usage](#bonus-usage)
  - [Error Handling](#error-handling)
- [Commands Used](#commands-used)
- [Important Files](#important-files)
- [What I Learned](#what-i-learned)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

---

## Overview  
Born2BeRoot is a system administration project that involves setting up a virtual machine with Debian, configuring it with strict security measures, and implementing a custom monitoring script. The project emphasizes understanding key Linux concepts such as SSH, UFW, sudo, and LVM. Additionally, the bonus part extends the project by setting up a functional WordPress site using Lighttpd, MariaDB, and PHP, and adding an additional service like LiteSpeed for improved performance.

---

## Features  
- **Virtual Machine Setup**: Installation and configuration of a Debian-based virtual machine using VirtualBox or VMware.
- **SSH Configuration**: Secure remote access to the VM with custom port settings and root login disabled.
- **UFW Firewall**: Implementation of Uncomplicated Firewall (UFW) to secure the VM, allowing only necessary ports.
- **Sudo Configuration**: Custom sudo rules with password policies, logging, and restricted access.
- **Monitoring Script**: A custom Bash script that monitors system resources (CPU, RAM, disk usage, etc.) and displays the information every 10 minutes via cron.
- **LVM Setup**: Logical Volume Management for flexible disk partitioning and management.

---

## Bonus Features  
- **WordPress Setup**: Installation and configuration of WordPress using Lighttpd as the web server, MariaDB as the database, and PHP for server-side scripting.
- **LiteSpeed**: Additional web server service for enhanced performance and security.
- **Partitioning**: Custom disk partitioning using LVM for better storage management.

---

## Requirements  
- **VirtualBox or VMware**: For creating and managing the virtual machine.
- **Debian ISO**: The operating system used for the VM.
- **SSH Client**: For remote access to the VM.
- **Basic Linux Knowledge**: Understanding of Linux commands, file systems, and network configurations.

---

## Summary of B2BR  
1. **Install VirtualBox or VMware**: Download and install a virtualization tool.
2. **Create a New VM**: Set up a new virtual machine using the Debian ISO.
3. **Install Debian**: Follow the installation steps, ensuring proper partitioning and LVM setup.
4. **Configure SSH**: Modify the SSH configuration file to change the default port and disable root login.
5. **Set Up UFW**: Install and configure UFW to allow only necessary ports (e.g., SSH on port 4242).
6. **Configure Sudo**: Set up custom sudo rules and password policies.
7. **Create Monitoring Script**: Write and schedule a Bash script to monitor system resources.
8. **Install WordPress (Bonus)**: Set up WordPress with Lighttpd, MariaDB, and PHP.
9. **Add LiteSpeed (Bonus)**: Install and configure LiteSpeed for enhanced web server performance.

### Example Usage

| **Input Command**                                      | **Description**                                                                 | **Expected Output**                                                                 |
|--------------------------------------------------------|---------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| `ssh user@localhost -p 4242`                           | Connect to the VM via SSH on port 4242.                                         | Successful SSH connection to the VM.                                               |
| `sudo ufw status`                                      | Check the status of the UFW firewall.                                           | List of active UFW rules, including port 4242.                                     |
| `./monitoring.sh`                                      | Run the monitoring script manually.                                             | Display system resource usage (CPU, RAM, disk, etc.).                              |

### Bonus Usage
For bonus features, follow these steps:

1. **Install Lighttpd, MariaDB, and PHP**:
   ```bash
   sudo apt install lighttpd mariadb-server php-cgi php-mysql
   sudo mysql_secure_installation
   ```

2. **Create a Database and User for WordPress**:
   ```bash
   sudo mariadb
   CREATE DATABASE wp_database;
   CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'password';
   GRANT ALL PRIVILEGES ON wp_database.* TO 'wp_user'@'localhost';
   FLUSH PRIVILEGES;
   exit
   ```

3. **Configure PHP for Lighttpd**:
   ```bash
   sudo lightly-enable-mod fastcgi
   sudo lightly-enable-mod fastcgi-php
   sudo service lighttpd restart
   ```

4. **Install WordPress**:
   ```bash
   cd /var/www
   sudo wget https://es.wordpress.org/latest-es_ES.zip
   sudo unzip latest-es_ES.zip
   sudo mv html/ html_old/
   sudo mv wordpress/ html
   sudo chmod -R 755 html
   ```

5. **Configure WordPress**:
   ```bash
   cd /var/www/html
   cp wp-config-sample.php wp-config.php
   nano wp-config.php
   ```
   - Update the following lines in `wp-config.php`:
     ```php
     define('DB_NAME', 'wp_database');
     define('DB_USER', 'wp_user');
     define('DB_PASSWORD', 'password');
     ```

6. **Install LiteSpeed**:
   ```bash
   sudo apt update
   sudo apt upgrade
   wget -O - https://repo.litespeed.sh | sudo bash
   sudo apt install openlitespeed
   sudo /usr/local/lsws/admin/misc/admpass.sh
   sudo ufw allow 8088/tcp
   sudo ufw allow 7080/tcp
   ```
---

## Commands Used  
Below is a list of the most important commands used in the project, organized into categories for clarity.

### General System Commands

| **Command**                     | **Description**                                                                 |
|---------------------------------|---------------------------------------------------------------------------------|
| `sudo apt update`               | Updates the package list from the repositories.                                |
| `sudo apt upgrade`              | Upgrades all installed packages to their latest versions.                      |
| `sudo apt install [package]`    | Installs a specific package (e.g., `sudo apt install openssh-server`).         |
| `sudo reboot`                   | Restarts the system.                                                           |
| `uname -a`                      | Displays system information (kernel version, architecture, etc.).              |
| `lsblk`                         | Lists all block devices (disks and partitions).                                |
| `df -h`                         | Displays disk space usage in a human-readable format.                          |
| `free -m`                       | Shows memory usage in megabytes.                                               |
| `who -b`                        | Displays the last system boot time.                                            |
| `hostname -I`                   | Shows the IP address of the system.                                            |
| `ip link`                       | Displays network interfaces and their MAC addresses.                           |

---

### SSH Configuration

| **Command**                     | **Description**                                                                 |
|---------------------------------|---------------------------------------------------------------------------------|
| `sudo apt install openssh-server` | Installs the SSH server.                                                      |
| `sudo nano /etc/ssh/sshd_config` | Edits the SSH configuration file.                                             |
| `sudo service ssh restart`       | Restarts the SSH service to apply configuration changes.                       |
| `ssh user@localhost -p 4242`     | Connects to the VM via SSH on port 4242.                                      |

---

### UFW Firewall Configuration

| **Command**                     | **Description**                                                                 |
|---------------------------------|---------------------------------------------------------------------------------|
| `sudo apt install ufw`          | Installs the UFW firewall.                                                     |
| `sudo ufw enable`               | Enables the UFW firewall.                                                      |
| `sudo ufw allow [port]`         | Allows traffic on a specific port (e.g., `sudo ufw allow 4242`).                |
| `sudo ufw delete allow [port]`  | Deletes the rule allowing traffic on a specific port.                          |
| `sudo ufw status`               | Displays the status of UFW rules (active rules and ports).                     |

---

### Sudo, User and Group Management

| **Command**                     | **Description**                                                                 |
|---------------------------------|---------------------------------------------------------------------------------|
| `sudo adduser [username]`       | Creates a new user with the specified username.                                 |
| `sudo addgroup [groupname]`     | Creates a new group with the specified group name.                              |
| `sudo adduser [username] [groupname]` | Adds a user to a specific group.                                           |
| `getent group [groupname]`      | Displays information about a specific group, including its members.             |
| `sudo deluser [username]`       | Deletes a user from the system.                                                |
| `sudo delgroup [groupname]`     | Deletes a group from the system.                                               |
| `sudo passwd [username]`        | Changes the password for a specific user.                                      |
| `sudo chage -l [username]`      | Displays password expiration information for a user.                           |
| `sudo chage -M [days] [username]` | Sets the maximum number of days between password changes for a user.         |
| `sudo chage -m [days] [username]` | Sets the minimum number of days between password changes for a user.         |
| `sudo chage -W [days] [username]` | Sets the number of days before password expiration to warn the user.         |
| `sudo visudo`                   | Edits the sudoers file to configure sudo permissions.                          |
| `sudo adduser [username] sudo`  | Adds a user to the `sudo` group, granting them sudo privileges.                |
| `sudo adduser [username] user42` | Adds a user to the `user42` group (if it exists).                             |
| `cat /etc/group`                | Displays all groups and their members on the system.                           |
| `sudo nano /etc/login.defs`     | Edits password policy settings (e.g., password expiration).                    |
| `sudo nano /etc/pam.d/common-password` | Configures password complexity rules (e.g., minimum length, uppercase).  |

---

### Monitoring Script and Cron

| **Command**                     | **Description**                                                                 |
|---------------------------------|---------------------------------------------------------------------------------|
| `nano monitoring.sh`            | Creates or edits the monitoring script.                                        |
| `chmod +x monitoring.sh`        | Makes the monitoring script executable.                                        |
| `crontab -e`                    | Edits the cron jobs to schedule tasks.                                         |
| `*/10 * * * * /path/to/monitoring.sh` | Adds a cron job to run the monitoring script every 10 minutes.            |

---

### WordPress Setup (Bonus)

| **Command**                     | **Description**                                                                 |
|---------------------------------|---------------------------------------------------------------------------------|
| `sudo apt install lighttpd mariadb-server php-cgi php-mysql` | Installs Lighttpd, MariaDB, and PHP.                                     |
| `sudo mysql_secure_installation` | Secures the MariaDB installation.                                             |
| `sudo mariadb`                  | Opens the MariaDB shell for database management.                               |
| `CREATE DATABASE wp_database;`  | Creates a new database for WordPress.                                          |
| `CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'password';` | Creates a new database user.                  |
| `GRANT ALL PRIVILEGES ON wp_database.* TO 'wp_user'@'localhost';` | Grants full privileges to the user for the WordPress database. |
| `FLUSH PRIVILEGES;`             | Reloads the privilege tables to apply changes.                                 |
| `sudo lightly-enable-mod fastcgi` | Enables the FastCGI module in Lighttpd for PHP support.                       |
| `sudo lightly-enable-mod fastcgi-php` | Enables PHP support via FastCGI in Lighttpd.                                |

---

### LiteSpeed Setup (Bonus)

| **Command**                     | **Description**                                                                 |
|---------------------------------|---------------------------------------------------------------------------------|
| `wget -O - https://repo.litespeed.sh | sudo bash` | Adds the LiteSpeed repository.                                |
| `sudo apt install openlitespeed` | Installs LiteSpeed.                                                            |
| `sudo /usr/local/lsws/admin/misc/admpass.sh` | Sets the LiteSpeed admin password.                              |
| `sudo ufw allow [port]`         | Allows traffic on a specific port (e.g., `sudo ufw allow 8088`).                |

---

## Important Files  
Below is a list of important files used in the project, along with their contents and purpose.

### SSH Configuration
- **`/etc/ssh/sshd_config`**: Configuration file for the SSH server.
  - Contains settings like the SSH port, root login permissions, and allowed authentication methods.
  - Modified to change the default port to 4242 and disable root login.

### UFW Firewall
- **`/etc/ufw/ufw.conf`**: Configuration file for the UFW firewall.
  - Contains basic settings like whether UFW is enabled or disabled.
  - Modified to enable UFW and allow specific ports (e.g., 4242 for SSH).

### Sudo Configuration
- **`/etc/sudoers`**: Configuration file for sudo permissions.
  - Contains rules for which users can execute commands with elevated privileges.
  - Modified to enforce password policies and logging for sudo commands.
- **`/etc/login.defs`**: Configuration file for login and password policies.
  - Contains settings like password expiration and minimum password length.
  - Modified to enforce strong password policies.
- **`/etc/pam.d/common-password`**: Configuration file for password complexity rules.
  - Contains settings for password requirements (e.g., minimum length, uppercase letters, etc.).
  - Modified to enforce strong password complexity.

### User and Group Configuration
- **`/etc/passwd`**: Contains user account information.
  - Lists all users on the system, including their home directories and default shells.
- **`/etc/group`**: Contains group information.
  - Lists all groups and their members.

### Monitoring Script
- **`monitoring.sh`**: Custom Bash script for monitoring system resources.
  - Contains commands to display CPU, RAM, disk usage, and other system information.
  - Scheduled to run every 10 minutes via cron.

### WordPress Configuration (Bonus)
- **`/var/www/html/wp-config.php`**: WordPress configuration file.
  - Contains database connection settings (e.g., database name, username, password).
  - Modified to connect WordPress to the MariaDB database.

### MariaDB Configuration (Bonus)
- **`/etc/mysql/mariadb.conf.d/50-server.cnf`**: Configuration file for MariaDB.
  - Contains settings like bind address, port, and database storage locations.
  - Modified to configure MariaDB for WordPress.

### PHP Configuration (Bonus)
- **`/etc/php/[version]/cgi/php.ini`**: Configuration file for PHP.
  - Contains settings like memory limits, file upload sizes, and error reporting.
  - Modified to optimize PHP for WordPress.

### LiteSpeed Configuration (Bonus)
- **`/usr/local/lsws/conf/httpd_config.conf`**: LiteSpeed configuration file.
  - Contains settings for the LiteSpeed web server, such as port numbers and virtual hosts.
  - Modified to configure LiteSpeed for optimal performance.

---

## What I Learned  
- **System Administration**: Gained hands-on experience with Linux system administration, including user management, firewall configuration, and service management.
- **Security Best Practices**: Learned how to secure a server by disabling root login, configuring UFW, and implementing strong password policies.
- **Scripting**: Developed a custom Bash script to monitor system resources and automate tasks using cron.
- **Virtualization**: Understood the process of setting up and managing virtual machines using VirtualBox and VMware.
- **User and Group Management**: Learned how to create and manage users and groups, including adding users to specific groups like `sudo` and `user42`.
- **Password Policies**: Gained experience in setting and enforcing password policies, including expiration dates and complexity requirements.
- **Sudo Configuration**: Understood how to configure sudo permissions and logging for users.
- **Web Server Configuration**: Gained experience in setting up and configuring web servers (Lighttpd, LiteSpeed) and databases (MariaDB) for WordPress.
- **Database Management**: Learned how to set up and manage MariaDB databases, including creating users and granting permissions.
- **PHP Configuration**: Configured PHP for use with Lighttpd and WordPress, including enabling FastCGI and optimizing PHP settings.

---

## Author  
- **Name**: Oliver King Zamora
- **GitHub**: [oliverkingz](https://github.com/oliverkingz)
- **42 Login**: ozamora-

---

## Acknowledgments  
This project is part of the **42 Cursus**, a rigorous programming curriculum that emphasizes hands-on learning and problem-solving. Special thanks to the 42 team for providing this challenging and rewarding project!  
Also thanks to peers and mentors for their feedback and support during the development process.

---
