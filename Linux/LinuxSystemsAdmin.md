## Linux Systems Administration

Step 1: Ensure/Double Check Permissions on Sensitive Files

1. Permissions on /etc/shadow should allow only `root` read and write access.

    - Command to inspect permissions: ls -l /etc/shadow
    - Command to set permissions (if needed): sudo chmod 600 /etc/shadow

  <i>*The numbers will vary according to permissions chosen for root, group, and others.</i>

2. Permissions on /etc/gshadow should allow only `root` read and write access.

    - Command to inspect permissions: ls -l /etc/gshadow
    - Command to set permissions (if needed): sudo chmod 600 /etc/gshadow

3. Permissions on /etc/group should allow `root` read and write access, and allow everyone else read access only. 

    - Command to inspect permissions: ls -l /etc/group    
    - Command to set permissions (if needed): sudo chmod 644 /etc/group

4. Permissions on /etc/passwd should allow `root` read and write access, and allow everyone else read access only.

    - Command to inspect permissions: ls -l /etc/passwd
    - Command to set permissions (if needed): sudo chmod 644 /etc/passwd

## Step 2: Create User Accounts

1. Add user accounts for `sam`, `joe`, `amy`, `sara`, and `admin`. 

    - Command to add each user account (include all five users): 

    sudo useradd <name> e.g.,

    sudo useradd sam
    sudo useradd joe