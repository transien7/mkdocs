# Creating an SSH Server
## Install SSH Server

1. On the machine that you want to accept remote connections from (i.e. the **server**)  
```
sudo apt install -y openssh-server
sudo systemctl status ssh               # check SSH server is running
sudo systemctl enable ssh               # if SSH server isn't running
sudo systemctl start ssh
```

2. Ensure the SSH service is running on the server:  
```
# with nmap
sudo apt install -y nmap
nmap -sV -p22 <ip_address>

# with ss
ss -ltr
```
## Create a key pair on the client

3. On the **client** machine, generate an RSA key-pair  
	Save the keys to the default directory with the default filenames, e.g. `/home/user/.ssh/id_rsa`  
```
ssh-keygen -t rsa -b 4096
```

4. Set the appropriate permissions:  
```
chmod 600 ~/.ssh/id_rsa     # private key
chmod 700 ~/.ssh            # .ssh directory
```
**NOTE:** Do not disable PasswordAuthentication in /etc/ssh/sshd_config on the server until the public key has been copied from the client
  
5. Copy the key to the remote server: 
```
ssh-copy-id -i id_rsa.pub -p 22 <username>@<hostname>
# enter password when prompted
# id_rsa.pub should be appended to the ~/.ssh/authorized_keys file on the remote server
```
## Configure the server

6. On the **server**, generate a host key:  
```
sudo ssh-keygen -A
```

7. Open the SSH server config file for editing:  
```
sudo vim /etc/ssh/sshd_config
```

9. Ensure the following options are set, removing any comments (`#`) where necessary:  
```
PubkeyAuthentication yes
PasswordAuthentication no
```

10. Finally, restart the SSH server:  
```
sudo systemctl restart ssh
```
## Log in to the SSH server

11. On the client machine, log in to the SSH server.  
	  **Note:**  
	  * `username` is the user on the remote machine  
	  * `hostname` is the remote machine's IP address:  
```
ssh username@hostname       # e.g. `ssh barry@192.168.1.50`
```

12. If authentication is successful, you should now see:  
```
barry@remote-machine:~$ 
```