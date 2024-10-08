# Installation Tutorial

## Installation

This section covers the detailed steps for installing MySQL 8.4 on Windows, macOS, and Linux. Each subsection will offer a clear explanation, practical examples, and step-by-step instructions, along with post-installation setup.

### Installing MySQL 8.4 on Windows

#### Step 1: Download MySQL Installer

1. **Go to the MySQL Downloads page:**
   - Navigate to the MySQL official website at [https://dev.mysql.com/downloads/installer/](https://dev.mysql.com/downloads/installer/).

2. **Select the MySQL Installer:**
   - Choose the `MySQL Installer for Windows` and download the `mysql-installer-web-community-8.4.x.msi` file.

#### Step 2: Run the Installer

1. **Open the Installer:**
   - Double-click the downloaded `.msi` file to launch the installer.

2. **Setup Type:**
   - You will be prompted to select a setup type. Choose `Custom` to customize the components you need or `Developer Default` for a comprehensive setup.

#### Step 3: Installation

1. **Select Products and Features:**
   - Ensure that `MySQL Server`, `MySQL Workbench`, and other desired components are selected.

2. **Check Requirements:**
   - The installer will check for any missing requirements. Install any necessary software, such as `Visual C++`, if prompted.

3. **Installation Progress:**
   - Click `Execute` to begin the installation of the selected components.

#### Step 4: Initial Configuration

1. **Configuration Type:**
   - Choose the `Standalone MySQL Server / Classic MySQL Replication` option.

2. **Server Configuration:**
   - Set the Config Type to `Development Computer`, `Server Computer`, or `Dedicated Computer`, based on your needs.
   - Choose the `Connectivity` options such as default port `3306`.

3. **Authentication Method:**
   - Select `Use Strong Password Encryption` for enhanced security.

4. **MySQL Root Password:**
   - Set a strong root password and add any additional MySQL users if necessary.

5. **Windows Service:**
   - Ensure that `Configure MySQL Server as a Windows Service` is checked. Optionally, set the service to start automatically.

#### Step 5: Complete Installation

1. **Execute Configuration:**
   - Click `Execute` to apply the configuration settings.

2. **Finish:**
   - Once the installation and configuration are complete, you will see a summary. Click `Finish`.

### Installing MySQL 8.4 on macOS

#### Step 1: Download MySQL DMG Archive

1. **Go to the MySQL Downloads page:**
   - Navigate to [https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/).

2. **Select macOS:**
   - Choose `macOS` and download the `dmg` file for MySQL 8.4.

#### Step 2: Install MySQL

1. **Open DMG File:**
   - Double-click the downloaded `.dmg` file to mount it.

2. **Run the Installer:**
   - Double-click the `mysql-8.4.x-macos10.x-x86_64.pkg` file.

3. **Follow Installer Steps:**
   - Follow the onscreen instructions in the install wizard.

4. **Authentication:**
   - During installation, you may be prompted to enter your macOS password to authorize the installation.

#### Step 3: Initial Configuration

1. **MySQL Preference Pane:**
   - After installation, a `MySQL` preference pane will be added to `System Preferences`.

2. **Start MySQL Server:**
   - Open `System Preferences` -> `MySQL` and click `Start MySQL Server`.

3. **Set Up Root Password:**
   - During initial startup, you will be prompted to set the root password.

#### Step 4: Add MySQL to System Path (Optional)

1. **Edit Profile:**
   - Open Terminal and edit your profile file (`~/.bash_profile` or `~/.zshrc`, depending on your shell).

2. **Add Path:**
   - Add the following line:
     ```bash
     export PATH=/usr/local/mysql/bin:$PATH
     ```

3. **Apply Changes:**
   - Source the profile by running:
     ```bash
     source ~/.bash_profile
     ```

### Installing MySQL 8.4 on Linux

#### Step 1: Update Package Repository

1. **Open Terminal:**
   - Open your terminal window.

2. **Update Package Lists:**
   - Run the following command to update your package lists:
     ```bash
     sudo apt update
     ```

#### Step 2: Install MySQL

1. **Add MySQL APT Repository:**
   - Download the MySQL APT repository package:
     ```bash
     wget https://dev.mysql.com/get/mysql-apt-config_0.8.17-1_all.deb
     ```
   - Install the MySQL APT config package:
     ```bash
     sudo dpkg -i mysql-apt-config_0.8.17-1_all.deb
     ```

2. **Update Package Lists Again:**
   - Run:
     ```bash
     sudo apt update
     ```

3. **Install MySQL Server:**
   - Install MySQL server:
     ```bash
     sudo apt install mysql-server
     ```

#### Step 3: Secure MySQL Installation

1. **Run Security Script:**
   - Execute the following command to run the security script:
     ```bash
     sudo mysql_secure_installation
     ```

2. **Follow Prompts:**
   - Follow the prompts to set the root password, remove anonymous users, disallow root login remotely, remove test databases, and reload privilege tables.

#### Step 4: Start MySQL Service

1. **Start Service:**
   - Ensure the MySQL service is running:
     ```bash
     sudo systemctl start mysql
     ```

2. **Enable Service to Start at Boot:**
   - Enable MySQL to start on boot:
     ```bash
     sudo systemctl enable mysql
     ```

### Post-Installation Setup

Regardless of your operating system, after installing MySQL 8.4, you should perform the following post-installation setup:

#### Step 1: Verify Installation

1. **Open Terminal or Command Prompt:**
   - Open your terminal (Linux/macOS) or Command Prompt (Windows).

2. **Log in to MySQL:**
   - Log in to MySQL using the root user:
     ```bash
     mysql -u root -p
     ```

3. **Check Version:**
   - Verify the MySQL version:
     ```sql
     SELECT VERSION();
     ```

#### Step 2: Create a Database and User

1. **Create Database:**
   - Create a new database:
     ```sql
     CREATE DATABASE mydatabase;
     ```

2. **Create User:**
   - Create a new user and grant privileges:
     ```sql
     CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';
     GRANT ALL PRIVILEGES ON mydatabase.* TO 'myuser'@'localhost';
     FLUSH PRIVILEGES;
     ```

#### Step 3: Exit MySQL

1. **Exit:**
   - Exit the MySQL command line:
     ```sql
     EXIT;
     ```

By following these detailed steps, you will have MySQL 8.4 installed and set up on your Windows, macOS, or Linux system, ready for further configuration and use.
