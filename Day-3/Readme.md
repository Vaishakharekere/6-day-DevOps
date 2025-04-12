# AWS Assignment Submission – IAM, EC2, CI/CD & Docker Setup


##  AWS IAM User Role

### Console Sign-in Link:
```
https://
```

### User Details:
- **User Name**: 
- **Console Password**: 



##  AWS EC2 – Launch Instance
1. Login to AWS Console.
2. Search for **EC2** and go to **EC2 Dashboard**.
3. Click on **Launch Instance**.
4. Configure the instance:
   - Choose AMI: Amazon Linux
   - Instance Type: `t2.micro`
   - Key pair: create/download key
   - Enable SSH (port 22) in network settings
5. Launch the instance.



##  CI/CD Pipeline

###  CI/CD Flow:
```
START -> INSTANCE (AWS LINUX) -> DEV -> POLICY (CI) -> EC2 INSTANCE -> Deploying the application -> END
```

###  Micro Pipelines:
- **Pipeline 2**: Adding more features


##  Creating a New IAM User
1. Go to **IAM** in AWS Console.
2. Under **Access Management**, select **Users**.
3. Click **Create User**.
4. Enter:
   - **Name**
   - **User access**: ✅ checked
   - Require password reset on first login: ✅ checked
5. Attach policies directly:
   - ✅ AdministratorAccess
6. Click **Next**, then **Create User**.
7. Use the Console Sign-in link, user name, and password to login as the new IAM user.


## Download PuTTY (For Windows users)
1. Search **PuTTY** in Google.
2. Download and install it.
3. Save it in **hard drive** (Option 2 in installer dropdown).
4. Set environment variable path (may be set automatically).
5. Open **PuTTY**:
   - **Host Name**: `ec2-user@<EC2_PUBLIC_IP>`
   - Go to **SSH > Auth > Credentials**:
     - Browse and select the `.ppk` file (created from key during instance setup).
6. Click **Open** to start session.



##  EC2 Console / PuTTY Interface
After connection:

### First Commands:
```bash
sudo
sudo yum update -y
```



##  Download & Install Docker
> Make sure PuTTY session is active before running commands.

### Docker Installation Steps:
```bash
sudo yum update -y
sudo yum install -y docker
sudo systemctl start docker
sudo systemctl enable docker
docker --version
```

### Expected Output (Example):
```bash
[ec2-user@ip-172-31-40-114 ~]$ docker --version
Docker version 25.0.8, build 0bab007
```

