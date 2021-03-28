## Linux Systems Administration

Step 1: Ensure/Double Check Permissions on Sensitive Files

1. Permissions on /etc/shadow should allow only `root` read and write access.

    - Command to inspect permissions: ls -l /etc/shadow
    - Command to set permissions (if needed): sudo chmod 600 /etc/shadow

  <i>*The numbers will vary according to permissions chosen for root, group, and others.</i>

  2. Permissions on /etc/gshadow should allow only `root` read and write access.

    - Command to inspect permissions: ls -l /etc/gshadow