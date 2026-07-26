# Webserver Project

A simple web server built using Nginx. This project documents the setup and deployment of a website on a Linux server.

The project covers:

- Connecting to a remote Linux server using SSH
- Securing SSH access with SSH keys
- Setting up Git access via SSH
- Installing and configuring Nginx
- Deploying a website to the web server

## Table of Contents
- [Establish a Connection to the Target Server](#establish-connection-to-the-target-server)
- [Establish Git Access via SSH](#estabilish-git-access-via-ssh)
- [Set Up Nginx](#set-up-nginx)
- [Webside Deployment](#webside-deployment)

## Establish a Connection to the Target Server

The first step is to establish a secure connection to the remote Linux server. SSH (Secure Shell) allows the client to remotely access and manage the server through the command line.

### 1. Generate an SSH Key

Client:

``
$ ssh-keygen -t ed25519
``


The command generates a private key and a public key.

The private key is stored locally and shouldn't never be shared. The public key can be safely copied to the server.

The generated files usually look like this, if the path and keyname won't changed:

``
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
``


### 2. Copy the Public Key to the Server

The public key can be copied to the server using:

´´
ssh-copy-id -i ~/.ssh/id_ed25519.pub username@SERVER_IP
´´
### 3. Connect Using the SSH Key

´´
ssh -i ~/.ssh/id_ed25519 username@SERVER_IP
´´

### 4. Disable Password Authentication


sudo nano /etc/ssh/sshd_config
PasswordAuthentication no
sudo systemctl restart ssh.service

> [!CAUTION]
> ⚠️ Make sure that SSH key authentication works before disabling password authentication. Otherwise, you may lose access to the server.
>


## Establish Git Access via SSH


## Set Up Nginx


## Webside Deployment
