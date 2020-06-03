# Set up SSH public-key authentication to connect to a remote system

## 1. Config (port, ...)
```
sudo nvim /etc/ssh/ssh_config
```
## 2. Generate RSA keys
```
ssh-keygen -t rsa
```
## 3. Get public key
Copy `~/.ssh/id_rsa.pub` to remote
## 4. On Remote system
### 4.1. If my account on the remote system doesn't already contain a `~/.ssh/authorized_keys` file, create one:
```
mkdir -p ~/.ssh
touch ~/.ssh/authorized_keys
```
### 4.2. Add the contents of my public key file `id_rsa.pub` to a new line in my `~/.ssh/authorized_keys` file:
```
cat id_rsa.pub >> ~/.ssh/authorized_keys
```
### 4.3 Now you can remove public key file `id_rsa.pub`
```
rm id_rsa.pub
```
### 4.4. Add more key (optional)
## 5. Config ssh on Remote system (port, AllowUsers ...)
### Edit config file:
```
sudo nvim /etc/ssh/sshd_config
```
### Start SSH service on remote system:
```
# systemctl start sshd.service
```
## 6. SSH on local network:
```
ssh remote-username@192.168.100.77 -p 1234
```
## 7. SSH between two different network
* My remote PC IP (internal): `192.168.100.77`
* Remote public IP (external): `123.123.123.123`
### Use `Port Mapping Configuration` or `Port Forward`... on my Modem Router:
* Internal Host: `My remote PC IP` (ex: 192.168.100.77)
* Internal port number: `ssh port` (ex: 1234)
* External port number: `port to modem router` (ex: 5678)
### How it works?
```
ssh remote-username@123.123.123.123 -p 5678
```
My PC >> port `5678` ip `123.123.123.123` >> port `1234` ip `192.168.100.77`
