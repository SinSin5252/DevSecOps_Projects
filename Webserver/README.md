# Webserver Project

A simple web server built using Nginx. This project documents the setup and deployment of a website on a Linux server.

The project covers:

- Connecting to a remote Linux server using SSH
- Securing SSH access with SSH keys
- Setting up Git access via SSH
- Installing and configuring Nginx
- Deploying a website to the web server

## Table of Contents

- [Establish a Connection to the Target Server](#establish-a-connection-to-the-target-server)
- [Establish Git Access via SSH](#establish-git-access-via-ssh)
- [Set Up Nginx](#set-up-nginx)
- [Webside Deployment](#webside-deployment)

## Establish a Connection to the Target Server

The first step is to establish a secure connection to the remote Linux server. SSH (Secure Shell) allows the client to remotely access and manage the server through the command line.

### 1. Generate an SSH Key

Client:

```bash
$ ssh-keygen -t ed25519
```

The command generates a private key and a public key.
The private key is stored locally and shouldn't never be shared. The public key can be safely copied to the server.
The generated files usually look like this, if the path and key name won't changed:


```bash 
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

During key generation, you will be prompted to enter a passphrase for the key. This serves as an additional layer of security. While entering a passphrase is optional, it is strongly recommended to protect your private key. If you choose to use one, store it securely in a password manager.


### 2. Copy the Public Key to the Server

The public key can be copied to the server using the following command:

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub username@SERVER_IP
```

### 3. Connect Using the SSH Key

The connection can be establish with the following command:

```bash
ssh -i ~/.ssh/id_ed25519 username@SERVER_IP
```

### 4. Disable Password Authentication

> [!CAUTION]
> ⚠️ Make sure that SSH key authentication works before disabling password authentication. Otherwise, you may lose access to the server.
>

Open the config file `sshd_config` with sudo rights and edit the value `PasswordAuthentication` to `no` (The # has to be removed). 

Server:
```bash
sudo nano /etc/ssh/sshd_config

```

Restart `ssh.service` after editing and saving the config file.

Server:
```bash
sudo systemctl restart ssh.service
```


## Establish Git Access via SSH

### 1. Generate an SSH Key for Git

The SSH key can be generated the same as in the previous [step](#1.-generate-an-ssh-key) and don't forget to use an other name for the key.

### 2. Link the SSH Key with Git

The content of the public key has to be copied to GitHub. 
```
cat ~/.ssh/<KEY_NAME>.pub
```

Go to the right top corner and click to your `Profil` and navigate to `Settings` in GitHub. Create a SSH Key under the menu `SSH and GPG Key`
enter the title and the copied key content.

### 3. Configure the SSH Key to solve Permission issues

If a permission denied error message appears after setup, the most issue is that the Server cant find the key. To solve this issue a `config` file has to be created.

```
touch ~/.ssh/config
```

The content of the `config` file is set as following:

```
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/<KEY_NAME>
    IdentitiesOnly yes
```


## Set Up Nginx


## Webside Deployment

