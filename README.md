# How-to-configure-Self-Hosted-Runner-in-GitHub-Actions
A step by step guide
I’m excited to share a recent task I successfully completed: configuring a Self-Hosted Runner for GitHub Actions on an AWS EC2 instance. 🎉
Below is a step-by-step guide I followed to help you set it up if you ever need it. Let’s dive right in!
================================================
🌟 Configure Self-Hosted GitHub Actions Runner on AWS EC2 Instance
A comprehensive guide to set up a self-hosted runner on an EC2 instance
================================================ 
 hashtag#Step 1: Launch an EC2 Instance
 1. Go to AWS Console / Instance Page
 2. Click Launch Instance.
 3. Choose an Amazon Machine Image (AMI), such as Amazon Linux 2 or Ubuntu.
 4. Select an Instance Type, e.g., t2.micro for testing purposes.
 5. Configure Instance Details:
 - Ensure the security group has access to SSH (port 22).
 8. Configure Security Group:
 - Allow inbound access to SSH (port 22) and HTTP/HTTPS (if needed).
 9. Launch the instance and download the key pair for SSH access.
 hashtag#Step 2: Access EC2 Instance
 1. Once the instance is running, connect to your EC2 instance via SSH:
 ssh -i "your-key.pem" ec2-user@<EC2-Public-IP>
 hashtag#Step 3: Install Dependencies
 1. Update the package manager:
 sudo yum update -y # For RHEL
 sudo apt update -y # For Ubuntu
 2. Install Git:
 sudo yum install git -y # For RHEL
 sudo apt install git -y # For Ubuntu
 
 hashtag#Step 4: Download GitHub Actions Runner
 1. Create a directory for the runner:
 mkdir actions-runner && cd actions-runner
 2. Download the runner package (replace `x64` with `arm64` for ARM instances):
 curl -o actions-runner-linux-x64.tar.gz -L https://lnkd.in/e2pu-ZdE
 3. Extract the package:
 tar xzf ./actions-runner-linux-x64.tar.gz
 hashtag#Step 5: Configure the Runner
 1. Get the self-hosted runner token:
 - Navigate to your GitHub repository.
 - Go to Settings > Actions > Runners > New Self-Hosted Runner.
 - Select Linux as the OS and follow the instructions to get the registration token.
 2. Run the configuration command on your EC2 instance:
 ./config.sh --url https://lnkd.in/eFMAvWiF --token <your-token>
 hashtag#Step 6: Install the Runner as a Service
 1. Install the runner as a service to ensure it starts automatically:
 sudo ./svc.sh install
 2. Start the runner:
 sudo ./svc.sh start
hashtag#Step 7: Verify the Runner
Go to your GitHub repository: Settings > Actions > Runners, and you should see your runner listed as online. ✅
 hashtag#Step 8: Use the Runner in a Workflow
 Create a GitHub Actions workflow that specifies runs-on: self-hosted to use the EC2 runner:
 name: Test Self-Hosted Runner
 
 on:
 push:
 branches:
 - main
 
 jobs:
 test:
 runs-on: self-hosted
 steps:
 - run: echo "Hello from the self-hosted runner!"
🎉 Congratulations! Your EC2 instance is now configured as a self-hosted GitHub Actions runner. I hope this guide helps you with your DevOps journey! 🚀
