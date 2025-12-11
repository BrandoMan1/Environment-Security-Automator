# Environment-Security-Automator
A secure, automated script that sets up a consistent development environment by installing required dependencies, generating project-specific configuration, and enforcing strict security permissions.
🎯 Purpose and Overview
The setup_dev_env.sh script automates the full setup and configuration of a standardized development environment on a newly provisioned server (Ubuntu/CentOS). It solves the critical problem of manual setup inconsistency by performing the following core actions:

Idempotent Dependency Installation: It checks for and installs required system dependencies (git, curl, jq, nginx).
Secure Configuration: It prompts the user for project details and securely generates a personalized configuration file (~/..config.yaml).
Security Enforcement: It ensures security by applying restrictive permissions (chmod 600) to the generated configuration and logs all execution steps for auditability.
🚀 Execution Guide
How to Run The script requires execution permission and should be run interactively by a user with sudo privileges (e.g., devops-brandon).

# Navigate to the Script:
cd members/brandon/
# Set Execution Permission (If Needed):
chmod +x setup_dev_env.sh
# Execute the Script:
./setup_dev_env.sh
💻 Example Interactive Session
The script requires interactive input for the project name and GitHub username, followed by the final success banner.

# Example command
./setup_dev_env.sh

# Example Input/Output Session
[... initial logging ...]
Enter your project name (e.g., frontend-api): Team4Tech-API-Service
Enter your GitHub username for configuration: BrandoMan
[... installation logs and success messages ...]

==================================================
✅ SETUP COMPLETE SUCCESSFULLY!
==================================================
Your personalized development environment is ready.

- Packages (git, curl, jq, nginx) verified.
- Configuration file created and secured: /home/devops-brandon/.Team4Tech-API-Service.config.yaml

🔥 Next Steps for BrandoMan:
    1. Clone your main project: git clone git@github.com:BrandoMan/Team4Tech-API-Service.git
    2. Start the application using your team's standard command.
    3. Review the complete log: ./dev_setup_YYYY-MM-DD.log
==================================================
📦 Dependencies and Requirements The setup_dev_env.sh script relies on the following packages and privileges to execute successfully:

Execution Requirements (Prerequisites)

Bash Shell: The script relies on the syntax and features of the standard Bash shell.
Root or Sudo Privileges: Required for package installation (apt / yum) and setting file permissions (chmod).
System Utilities (Assumed Pre-installed) These utilities are used for core script logic and logging:

sed: Used for in-place text replacement during configuration file templating.
tee: Used within the logging function to write messages to both the console and the log file simultaneously.
date: Used for timestamping log messages and creating unique log/backup file names.
command -v: Used for checking if packages are already installed (idempotency check).
mkdir: Used to ensure the log directory exists..
Mitigation if Missing

If any of these core utilities are reported as "Command not found" (which can happen on minimal server images), you may need to install the GNU coreutils package, which contains most of these standard binaries.
# For Ubuntu/Debian (Recommended for your EC2 server):
sudo apt update && sudo apt install coreutils -y
Required Packages (Installed by Script)

The script automatically checks for and installs these packages if they are missing: git, curl, jq, and nginx.
