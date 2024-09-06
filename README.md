# Automated S.M.A.R.T. Test with Email Notifications

## Overview

This repository contains a Bash script designed to run a **S.M.A.R.T. (Self-Monitoring, Analysis, and Reporting Technology)** test on your Linux system's hard drives and automatically email the results using an SMTP server. The script is compatible with both **RHEL-based distributions** (like CentOS, Fedora, etc.) and **Ubuntu-based distributions**.

## Features
- Runs a S.M.A.R.T. test on a specified disk (supports both short and long tests).
- Sends test results via email to a configured address.
- SMTP authentication support with configurable server, port, and credentials.
- Works across various Linux distributions.

## Prerequisites

Ensure that `smartmontools` and `mailx` (or `mailutils` on Ubuntu) are installed. Use the following commands based on your distribution:

For **RHEL-based** distributions:
```bash
sudo yum install smartmontools mailx
```

For **Ubuntu-based** distributions:
```bash
sudo apt install smartmontools mailutils
```

## Setup

1. Clone this repository to your local machine:
   ```bash
   git clone https://github.com/yourusername/smart-test-email-script.git
   ```

2. Navigate to the project directory:
   ```bash
   cd smart-test-email-script
   ```

3. Modify the variables in the script to suit your environment:
   - `EMAIL`: Recipient email address.
   - `FROM_EMAIL`: Sender email address.
   - `SMTP_SERVER`: Your SMTP server (e.g., `smtp.gmail.com`).
   - `SMTP_PORT`: Port number (commonly `587` for TLS).
   - `SMTP_USER` and `SMTP_PASS`: Your SMTP username and password.

4. Make the script executable:
   ```bash
   chmod +x smart_test_email.sh
   ```

5. Run the script:
   ```bash
   ./smart_test_email.sh
   ```

## Customization

### Change Disk Device
By default, the script checks `/dev/sda`. If your system uses a different disk, modify the `DEVICE` variable in the script:
```bash
DEVICE="/dev/nvme0n1"
```

### Test Type
By default, the script runs a **short S.M.A.R.T. test**. If you want to run a longer test, change the following line in the script:
```bash
smartctl --test=long $DEVICE
```

## Running the Script Automatically Every 7 Days

You can automate the script to run every 7 days using **cron**.

### Steps to Set Up a Cron Job:

1. **Open the crontab**:
   ```bash
   crontab -e
   ```

2. **Add the following cron job** to run the script every 7 days:
   ```bash
   0 0 */7 * * /path/to/smart_test_email.sh
   ```

   - This line schedules the script to run at **midnight (00:00)** every 7 days.
   - Replace `/path/to/smart_test_email.sh` with the actual path to your script.

3. **Save and exit** the crontab editor.

After this, the S.M.A.R.T. test will automatically run every 7 days, and you'll receive the email with the test result.

## Example

Here’s an example of how to run the script manually:
```
./smart_test_email.sh
```
Once the test is complete, you will receive an email with the S.M.A.R.T. test results.

## Contribution

Feel free to open issues, submit pull requests, or suggest improvements!
