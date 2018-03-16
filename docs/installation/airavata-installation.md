# Apache Airavata Installation

[TOC]

## Introduction

!!! note
    **Apache Airavata 0.17** uses [Ansible](http://docs.ansible.com/ansible/latest/index.html) for its installation. This documentation gives a **step-by-step** guide to install Apache Airavata 0.17 using [Ancible Playbooks](http://docs.ansible.com/ansible/latest/playbooks.html).

**Apache Airavata** is a software framework that enables you to compose, manage, execute, and monitor large scale applications and workflows on distributed computing resources such as local clusters, supercomputers,computational grids, and computing clouds.

**[Ansible](http://docs.ansible.com/ansible/latest/index.html)** is a software tool that automates software provisioning, configuration management, and application deployment. Unlike many other alternatives, Ansible is installed on a single host (which can even be your local machine), and uses **Secure Shell (SSH)** to communicate with each remote host, without a need of any prerequisite package to be installed on each new server.

## Prerequisites

!!! warning
    **Apache Airavata 0.17** installation is only supported for [CentOS](https://www.centos.org/) 7 or never versions.

### CentOS 7 Server / VM / Docker Container

To install Apache Airavata a CentOS 7 environment is required. If the OS is behind a firewall, TCP ports: `443`, `3306`, `8008`, `8080`, `8962` and `9930` should be opened.

!!! note
    CentOS is an open source Linux distribution compatible with its upstream source, Red Hat Enterprise Linux (RHEL).

#### Install and Enable Your Firewall to Start at Boot

firewalld is installed by default on many images of CentOS 7. You can check the status using the following command.

```
firewall-cmd --state
```

!!! note
    [firewalld](http://www.firewalld.org/documentation/) is a firewall management tool for Linux operating systems.

If firewall is not installed please install and enable it before continuing.

### Python3 in Local Machine

Before continuing from this point you should verify the installed version of Python3 in your local machine. Use the following command to check the version.

```
python3 --version
```

If python3 is not already installed, the latest version should be installed. Refer [this](https://www.python.org/downloads/) or use your system’s package manager. Then install Python developer package using the following command.

```
sudo apt install python3-dev
```

## Configuration

In your local machine clone Apache Airavata from the [GitHub repository](https://github.com/apache/airavata).

```
git clone https://github.com/apache/airavata.git
```

<!-- ### Variable Configuration -->
<!-- Need to add -->

### Host Configuration

Go to the `airavata/dev-tools/ansible/inventories/standalone` directory and modify the `hosts` file. Update the `CHANGEME`s to the actual IP addresses or hostnames.

```
---
# inventory file
# NOTE: update the CHANGEMEs to the actual ip address or hostname.

[zookeeper]
CHANGEME ansible_connection=ssh ansible_user=root

[rabbitmq]
CHANGEME ansible_connection=ssh ansible_user=root

[database]
CHANGEME ansible_connection=ssh ansible_user=root

[api-orch]
CHANGEME ansible_connection=ssh ansible_user=root

[gfac]
CHANGEME ansible_connection=ssh ansible_user=root

[pga]
CHANGEME ansible_user=root

[keycloak]
CHANGEME ansible_connection=ssh ansible_user=root

```

### Keycloak Key Generation

Navigate to the `airavata/dev-tools/ansible/inventories/standalone/` directory and create a directory named `files`.

```
cd airavata/dev-tools/ansible/inventories/standalone/
mkdir files
cd files/
```

Then run the following command within the `files` directory.

```
keytool -genkey -keyalg RSA -alias selfsigned -keystore keystore.jks -storepass [password] -validity 360 -keysize 2048
```

`[password]` should be provided as specified at `airavata/dev-tools/ansible/inventories/standalone/group_vars/all/vars.yml` as `keystore_passwd`.

Provide the requested information when prompted and at the end when the following appears just press `enter`.

```
Enter key password for <selfsigned> 
        (RETURN if same as keystore password):
```

After that, run the following command and for prompted passwords, provide the above `keystore_passwd`.

```
keytool -importkeystore -srckeystore keystore.jks -destkeystore airavata.jks -deststoretype pkcs12
```

Now your `airavata/dev-tools/ansible/inventories/standalone/files` should have two files, `airavata.jks` and `keystore.jks`. You have to remove the file `keystore.jks`.

```
rm keystore.jks
```

### Airavata Key Generation

Run the following command from `airavata/dev-tools/ansible/inventories/standalone/files`.

```
keytool -export -alias selfsigned -file root.cer -keystore airavata.jks -storepass [password]
```

`[password]` should be provided as specified at `airavata/dev-tools/ansible/inventories/standalone/group_vars/all/vars.yml` as `keystore_passwd`.

```
keytool -import -alias mykey -file root.cer -keystore client_truststore.jks -storepass [password]
```

`[password]` should be provided as specified at `airavata/dev-tools/ansible/inventories/standalone/group_vars/all/vars.yml` as `client_truststore_passwd`.

When the following appears provide `yes` to trust the certificate.

```
Trust this certificate? [no]:
```

Now your `airavata/dev-tools/ansible/inventories/standalone/files` should have two files, `airavata.jks`, `client_truststore.jks` and `root.cer`. You have to remove file `root.cer`.

```
rm root.cer
```

### Airavata Key Store Generation

Run the following command from `airavata/dev-tools/ansible/inventories/standalone/files`.

```
keytool -genseckey -alias seckey -keyalg AES -keysize 128 -storetype jceks -keystore cred_store.jks -storepass [password]
```

`[password]` should be provided as specified at `airavata/dev-tools/ansible/inventories/standalone/group_vars/all/vars.yml` as `cred_keystore_passwd`.

When the following appears just press `enter`.

```
Enter key password for <seckey>
        (RETURN if same as keystore password):
```

### Ansible Installation

First of all we have to create a Python3 virtual environment at the `airavata/dev-tools/ansible` directory.

```
cd airavata/dev-tools/ansible
python3.6 -m venv ENV
```

To use the created virtual environment you have to source the environment. Remember to do this every time you want to use this python virtual environment.

```
source ENV/bin/activate
```

Now it’s time to install Ancible.

```
pip install -r requirements.txt
```

## Deployment

To start the deployment go to the `airavata/dev-tools/ansible` directory, and source the python virtual environment, if you haven't done it already.

### Database Installation

```
ansible-playbook -i inventories/standalone database.yml
```

### Keycloak Installation

!!! note
    [Keycloak](https://www.keycloak.org/documentation.html) is an open source Identity and Access Management solution.

```
ansible-playbook -i inventories/standalone keycloak.yml --tags="standalone"
```

### Keycloak Configuration

Use [this](../configuration/keycloak-configuration.md) guide to configure Keycloak.

### Airavata + RabbitMQ + Zookeeper Installation

```
ansible-playbook -i inventories/standalone airavata.yml
```

### PGA Installation

```
ansible-playbook -i inventories/standalone pga.yml
```

Now you can access PGA through the following URL. (Replace **<vm-ip\>** with the actual IP address of the server)

```
http://<vm-ip>:8008/
```

Login with `admin_username` and `admin_password`.

`admin_username` and `admin_password` should be used as specified at `airavata/dev-tools/ansible/inventories/standalone/group_vars/pga/vars.yml` as `admin_username` and `admin_password` respectively.
