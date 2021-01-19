# DevOps Interview Project

This project demonstrates a local development environment setup using Vagrant, Docker, and Ansible. It creates a virtual machine running two Apache web servers behind an Nginx reverse proxy, all containerized using Docker.

## Project Overview

The setup consists of:
- A Vagrant-managed Ubuntu 20.04 LTS virtual machine
- Two Apache web servers running in Docker containers
- An Nginx reverse proxy (also in a Docker container) routing traffic to the Apache servers
- Ansible for automating the provisioning and configuration of the environment

## Prerequisites

- [Vagrant](https://www.vagrantup.com/downloads) (2.2.x or later)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads) (6.1.x or later)
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) (2.9.x or later, installed on your host machine)

## Project Structure

- `Vagrantfile`: Defines the virtual machine configuration and provisioning steps
- `main.yml`: Ansible playbook for setting up Docker containers and testing the setup
- `docker-compose.yml`: Defines the Docker services (Nginx and Apache containers)
- `nginx.conf`: Nginx reverse proxy configuration
- `index1.html`, `index2.html`: Sample web pages for Apache containers

## Installation and Setup

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/devops-interview-project.git
   cd devops-interview-project
   ```

2. Start the Vagrant VM and provision it:
   ```
   vagrant up 2>&1 | tee vagrant.log
   ```
   This command will create the VM, install necessary software, and run the Ansible playbook to set up the Docker containers.

## Usage

After the installation is complete, you can access the web servers at:
- http://192.168.56.10/web1/
- http://192.168.56.10/web2/

Replace `192.168.56.10` with the IP address specified in your Vagrantfile if you've modified it.

Accessing just the vagrant box ip address will forward you request randomly to either web1 or web2 backends.

## Testing

To manually test the setup:

1. SSH into the Vagrant VM:
   ```
   vagrant ssh
   ```

2. Run the Ansible playbook:
   ```
   ansible-playbook /vagrant/main.yml
   ```

This will run through the setup steps and perform tests to ensure the web services are accessible.

## Troubleshooting

If you encounter issues:

1. Ensure all prerequisites are correctly installed.
2. Check the Vagrant and Ansible output for specific error messages.
3. Verify that the Docker containers are running inside the VM:
   ```
   vagrant ssh -c "docker ps"
   ```
4. Check the Nginx logs:
   ```
   vagrant ssh -c "docker logs nginx"
   ```

## Customization

- To modify the web content, edit `index1.html` and `index2.html`.
- To change the Nginx configuration, modify `nginx.conf`.
- To alter the Docker setup, edit `docker-compose.yml`.

## Cleaning Up

To stop and remove the Vagrant VM:
    ```
    vagrant destroy -f
    ```