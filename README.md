# RabbitMQ Installation Guide

This guide provides step-by-step instructions to install RabbitMQ on various platforms: Linux, macOS, and Windows.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
  - [Installing RabbitMQ on Debian/Ubuntu (Linux)](#installing-rabbitmq-on-debianubuntu-linux)
  - [Installing RabbitMQ on CentOS/RHEL (Linux)](#installing-rabbitmq-on-centosrhel-linux)
  - [Installing RabbitMQ on macOS](#installing-rabbitmq-on-macos)
  - [Installing RabbitMQ on Windows](#installing-rabbitmq-on-windows)
- [Post-Installation Configuration](#post-installation-configuration)
- [Starting and Managing RabbitMQ](#starting-and-managing-rabbitmq)
- [Accessing the Management Interface](#accessing-the-management-interface)
- [Uninstallation](#uninstallation)

## Prerequisites

Before installing RabbitMQ, ensure that your system meets the following requirements:

- **Erlang/OTP:** RabbitMQ requires Erlang/OTP to run. Make sure to install a compatible version. Erlang can be installed via your platform's package manager or by downloading from the [Erlang Solutions website](https://www.erlang-solutions.com/resources/download.html).

## Installation

### Installing RabbitMQ on Debian/Ubuntu (Linux)

1. **Update your package list:**

    ```bash
    sudo apt-get update
    ```

2. **Install Erlang:**

    ```bash
    sudo apt-get install -y erlang
    ```

3. **Add the RabbitMQ APT repository:**

    ```bash
    echo "deb https://dl.bintray.com/rabbitmq/debian $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/bintray.rabbitmq.list
    ```

4. **Import the RabbitMQ public key:**

    ```bash
    wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | sudo apt-key add -
    ```

5. **Install RabbitMQ server:**

    ```bash
    sudo apt-get update
    sudo apt-get install -y rabbitmq-server
    ```

### Installing RabbitMQ on CentOS/RHEL (Linux)

1. **Enable the EPEL repository:**

    ```bash
    sudo yum install epel-release -y
    ```

2. **Install Erlang:**

    ```bash
    sudo yum install -y erlang
    ```

3. **Add the RabbitMQ RPM repository:**

    ```bash
    sudo rpm --import https://packagecloud.io/rabbitmq/rabbitmq-server/gpgkey
    sudo tee /etc/yum.repos.d/rabbitmq_rabbitmq-server.repo <<EOF
    [rabbitmq_rabbitmq-server]
    name=rabbitmq_rabbitmq-server
    baseurl=https://packagecloud.io/rabbitmq/rabbitmq-server/el/7/$basearch
    gpgcheck=1
    gpgkey=https://packagecloud.io/rabbitmq/rabbitmq-server/gpgkey
    enabled=1
    EOF
    ```

4. **Install RabbitMQ server:**

    ```bash
    sudo yum install -y rabbitmq-server
    ```

### Installing RabbitMQ on macOS

1. **Install Homebrew (if not already installed):**

    If you do not have Homebrew installed, you can install it with the following command:

    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

2. **Install RabbitMQ via Homebrew:**

    ```bash
    brew install rabbitmq
    ```

3. **Start the RabbitMQ service:**

    ```bash
    brew services start rabbitmq
    ```

4. **Verify the installation:**

    You can verify that RabbitMQ is running by checking the service status:

    ```bash
    brew services list
    ```

### Installing RabbitMQ on Windows

1. **Download RabbitMQ:**

    Download the RabbitMQ installer from the [official RabbitMQ website](https://www.rabbitmq.com/install-windows.html).

2. **Install Erlang/OTP:**

    Download and install Erlang/OTP from [Erlang Solutions](https://www.erlang-solutions.com/resources/download.html). Ensure the installation directory is added to the system's PATH environment variable.

3. **Run the RabbitMQ installer:**

    - Execute the RabbitMQ installer and follow the on-screen instructions.
    - Ensure that the installer can find the Erlang installation path.

4. **Set up environment variables:**

    Ensure the RabbitMQ service can locate the Erlang installation by setting the `ERLANG_HOME` environment variable to your Erlang installation path (e.g., `C:\Program Files\erlXX.X`).

5. **Start RabbitMQ service:**

    After installation, start RabbitMQ using the Windows Services management console or by running the following command:

    ```cmd
    rabbitmq-service.bat install
    rabbitmq-service.bat start
    ```

## Post-Installation Configuration

1. **Enable the RabbitMQ management plugin:**

    The management plugin provides a web-based UI for managing RabbitMQ. Enable it with the following command:

    ```bash
    sudo rabbitmq-plugins enable rabbitmq_management
    ```

2. **Create a user and set permissions (optional):**

    It's a good practice to create a new user and assign appropriate permissions:

    ```bash
    sudo rabbitmqctl add_user myuser mypassword
    sudo rabbitmqctl set_user_tags myuser administrator
    sudo rabbitmqctl set_permissions -p / myuser ".*" ".*" ".*"
    ```

## Starting and Managing RabbitMQ

### Linux

- **Start RabbitMQ:**

    ```bash
    sudo systemctl start rabbitmq-server
    ```

- **Enable RabbitMQ to start on boot:**

    ```bash
    sudo systemctl enable rabbitmq-server
    ```

### macOS

- **Start RabbitMQ with Homebrew:**

    ```bash
    brew services start rabbitmq
    ```

### Windows

- **Start RabbitMQ via Command Prompt:**

    ```cmd
    rabbitmq-service.bat start
    ```

- **Stop RabbitMQ via Command Prompt:**

    ```cmd
    rabbitmq-service.bat stop
    ```

## Accessing the Management Interface

After enabling the management plugin, you can access the RabbitMQ Management Interface via your web browser:

- **URL:** `http://localhost:15672`
- **Default Credentials:**
  - **Username:** guest
  - **Password:** guest

## Uninstallation

### Uninstalling RabbitMQ on Linux

- **Debian/Ubuntu:**

    ```bash
    sudo apt-get remove --purge rabbitmq-server
    ```

- **CentOS/RHEL:**

    ```bash
    sudo yum remove rabbitmq-server
    ```

### Uninstalling RabbitMQ on macOS

1. **Stop the RabbitMQ service:**

    ```bash
    brew services stop rabbitmq
    ```

2. **Uninstall RabbitMQ:**

    ```bash
    brew uninstall rabbitmq
    ```

### Uninstalling RabbitMQ on Windows

1. **Stop the RabbitMQ service:**

    ```cmd
    rabbitmq-service.bat stop
    ```

2. **Uninstall RabbitMQ:**

    Use the "Add or Remove Programs" feature in Windows to uninstall RabbitMQ.

---

By following these instructions, you should be able to install and manage RabbitMQ on your chosen platform successfully.
