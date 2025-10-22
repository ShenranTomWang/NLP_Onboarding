# SSH Key Tutorial
This document will walk you through how you can add a ssh key to a server.

## What is a SSH Key?
A ssh key is a string that is used for the server to identify your computer.

## Why Adding a SSH Key?
Adding your computer's ssh key to the server so you don't have to enter your password each time you log in to that server.

## Adding your SSH Key to a Server
1. On your local computer, open a terminal and run: `ssh-keygen -t rsa`. Press `enter` if it prompts you anything. Your ssh key will be saved to `~/.ssh/id_rsa.pub` on your local computer.
2. Log in to the server, open `~/.ssh/authorized_keys` and paste your ssh key there.