# Install Certbot on Ubuntu

To install Certbot on Ubuntu, please follow the steps outlined below

## ***Step 1. Ensure that your version of snapd is up to date***

To update snapd, run the following command:

```Bash
sudo snap install core; sudo snap refresh core
```

*By executing this command with administrative privileges (sudo), you are explicitly allowing Certbot plugins to have root-level access. This means that the plugins can perform certain privileged operations and interact with system components that are typically restricted to administrative users*

You will see an output similar to:

```Bash
ubuntu@T3SCP:~$ sudo snap install core; sudo snap refresh core
core 16-2.58.3 from Canonical✓ installed
snap "core" has no updates available
```

## ***Step 2. Remove certbot-auto and any Certbot OS packages***

If certbot or any Certbot OS packages are already installed, remove them using the following command:

```Bash
sudo apt remove certbot
```

The output will show that the package has been successfully removed, or if certbot is not installed, it will inform you that it is not found

```Bash
ubuntu@T3SCP:~$ sudo apt remove certbot
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package 'certbot' is not installed, so not removed
0 upgraded, 0 newly installed, 0 to remove and 9 not upgraded.
```

## ***Step 3. Install Certbot***

To install Certbot, execute the following command:

```Bash
sudo snap install --classic certbot
```

The output will confirm the installation of Certbot

```Bash
ubuntu@T3SCP:~$ sudo snap install --classic certbot
certbot 2.6.0 from Certbot Project (certbot-eff✓) installed
```

## ***Step 4. Prepare the Certbot command***

Create a symbolic link for the Certbot command with the following command:

```Bash
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

This step ensures that the Certbot command can be executed conveniently from the command line.

## ***Step 5. Confirm plugin containment level***

To ensure the security and integrity of the Certbot plugin system, a plugin containment level needs to be set. This containment level determines the trust and privileges granted to Certbot plugins when they interact with the system

To confirm the plugin containment level and grant the necessary privileges, you can use the following command:

```Bash
sudo snap set certbot trust-plugin-with-root=ok
```

Setting the containment level to "ok" ensures that Certbot plugins have the necessary permissions to carry out their tasks effectively. This can include actions such as modifying system configurations, managing cryptographic keys, or interacting with network services securely

>***By following these steps, you can successfully install Certbot on your Ubuntu system. Certbot provides a user-friendly and efficient way to manage SSL/TLS certificates, enabling secure communication over the internet***