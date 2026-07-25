# Webserver Project

A simple web server built using Nginx. This project documents the setup of a website on a Linux server.

## Table of Contents
- [Establish connection to the target server](#establish-connection-to-the-target-server)

## Establish connection to the target server

After ensuring the connectivity over the login credentials, it is recomendet to connect with a ssh key. After ensuring that the ssh key works, deactivate the authenticaton over login credentials to protect the server from brutforce. to generate a ssh key following comands will be used in Linux shell:

generate a ssh key

1. Generation
Client:

``
$ ssh-keygen -t ed25519
``
2. 
