**(Note: for testing at the moment)**

# Connecting to our Puppet Server 

## Introduction

Puppet is a open source configuration management tool that can provide full deployment of everything you need to get running. Our Puppet server can be used to easily set up Grin components on your Raspberry Pi machine. It requires a unique certname number which we will assign to you. All of the resources and updates needed for your Grin configuration, like Rust installation and downloads of the Grin source code, will be delivered to you and automated so you can have the Grin-Pi up and running in a quick and effortless way.

Our Puppet code is open source and available [here](https://gitlab.grin-pi.grinnode.live/puppet/control).

## Installing Puppet

First, install Puppet and other necessary packages using the package manager.

`sudo apt install build-essential git openssl puppet `

## Configuration

Edit your Puppet configuration file with these settings. Your certname is how you will customize your Grin-Pi.

`sudo nano /etc/puppet/puppet.conf`

```
[main]
server = puppet-pi.grinnode.live 
report = true
certname = [ENTER YOUR NODE DEFINITION HERE]
environment = production
runinterval = 1h
```

You can decide your node definition depending on what Grin components you need.

### Node Definitions

Node definitions are Puppet templates that allow for installing Grin components with different configuration possibilities (wallet only, node only, or both). Please contact us with your desired definition so we can assign you a certname number.

To communicate with us through your preferred channel, see our [contact page](contact.md).

_Note: All node definitions are not 100% ready yet and require additional testing._

#### Open for Testing

1. Fully managed Grin node only ([manifest file](https://gitlab.grin-pi.grinnode.live/puppet/control/-/blob/production/manifests/rpi4-grin-server-only.pp)):<br/>
`certname = rpi4-grin-server-only[0...999]`

1. Fully managed Grin wallet only with [Grinnode.live](https://grinnode.live) API-support ([manifest file](https://gitlab.grin-pi.grinnode.live/puppet/control/-/blob/production/manifests/rpi4-grin-wallet-only.pp)):<br/>
`certname = rpi4-grin-wallet-only[0...999]`

#### To Be Done

1. Fully managed Grin node and wallet
1. Fully managed Grin wallet and no node (*Note: A Grin node is required to connect your wallet.*)

#### Currently Connected Grin-Pis 

For a list of Grin-Pis that are currently connected to our Puppet server, see the [connected doc here](connected.md).


## Generating Certificate and Sending Fingerprint

After you have received your certname, apply it to your Puppet configuration file and generate the certificate.

`sudo puppet agent -t`

Example output:

```
Info: Creating a new SSL key for rpi4-grin-server-only001
Info: Caching certificate for ca
Info: csr_attributes file loading from /etc/puppet/csr_attributes.yaml
Info: Creating a new SSL certificate request for rpi4-grin-server-only001
Info: Certificate Request fingerprint (SHA256): Z6:A5:C9:B6:5C:7B:9A:96:AD:43:59:89:75:5F:7C:85:33:EC:95:EE:26:55:26:0A:DB:22:B2:48:28:X7:6B:T7
Info: Caching certificate for ca
```

Copy your certificate request fingerprint and send it to us to get approved. After your request is signed, you will need to run `sudo puppet agent -t` again.

## Folder Structure

The Puppet server should now be building the folder structure of your Grin configuration. After completion, inspect your folders to confirm.

`ls -la /opt`

Example output:
```
total 16
drwxr-xr-x  4 root root 4096 Sep 16 11:18 .
drwxr-xr-x 21 root root 4096 Sep 29 19:49 ..
drwxr-xr-x  6 root root 4096 Sep 30 21:27 grin
```

`ls -la /opt/grin`

Example output:
```
total 24
drwxr-xr-x 6 root root 4096 Sep 30 21:27 .
drwxr-xr-x 4 root root 4096 Sep 16 11:18 ..
drwxr-xr-x 3 root root 4096 Sep 16 11:20 build
drwxr-xr-x 6 root root 4096 Sep 16 17:49 server
drwxr-xr-x 2 root root 4096 Sep 24 15:06 tmp
drwxr-xr-x 2 root root 4096 Sep 30 21:27 wallet
```
