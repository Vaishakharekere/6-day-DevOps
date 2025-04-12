# Devops Training - Day 2 : AWS EC2 Setup and Basic Linux Commands

##  AWS Account Creation
1. Go to [https://aws.amazon.com/](https://aws.amazon.com/)
2. Click on **“Create an AWS Account”**
3. Fill in the following:
   - Email address
   - Password
   - AWS account name
4. Set **account type** (choose "Personal" unless instructed otherwise)
5. Enter billing information (credit/debit card required)
6. Choose a **support plan** (select the **Free Basic Plan**)
7. Wait for the account to be verified and activated



## Launching an EC2 Instance
1. Sign in to your [AWS Management Console](https://console.aws.amazon.com/)
2. Navigate to **EC2 Dashboard** (search for "EC2" in the top search bar)
3. Click **"Launch Instance"**
4. Configure:
   - **Name**: `day2-ec2-instance`
   - **AMI**: Amazon Linux 2023 or Amazon Linux 2
   - **Instance type**: `t2.micro` (Free Tier eligible)
   - **Key pair**: Create new key pair (e.g., `day2-key`) and download the `.pem` file
   - **Network settings**: Allow **SSH (port 22)**
5. Click **Launch Instance**
6. Once launched, go to **Instances > Connect**
   - Select **SSH client**
   - Copy the provided SSH command



##  Connecting to Your EC2 Instance

In your terminal, run:

```bash
chmod 400 path/to/day2-key.pem
ssh -i path/to/day2-key.pem ec2-user@<your-ec2-public-ip>
```

> Replace `path/to/day2-key.pem` with the actual path and `<your-ec2-public-ip>` with your instance’s IP address.


## Updating AWS Linux Packages

After connecting to your instance, run:

### For Amazon Linux 2:
```bash
sudo yum update -y
```

### For Amazon Linux 2023:
```bash
sudo dnf update -y
```



##  Linux Commands Practiced

| Command         | Description                              |
|-----------------|------------------------------------------|
| `ls`            | Lists files and directories              |
| `pwd`           | Prints current directory path            |
| `cd <dir>`      | Change to directory `<dir>`              |
| `touch <file>`  | Creates an empty file named `<file>`     |
| `mkdir <dir>`   | Creates a directory named `<dir>`        |
| `rm <file>`     | Deletes the specified file               |
| `rmdir <dir>`   | Deletes an empty directory               |
| `sudo`          | Run a command with superuser privileges  |
| `clear`         | Clears the terminal screen               |
| `exit`          | Logs out from the SSH session            |




