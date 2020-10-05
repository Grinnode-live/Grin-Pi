**(Note: for testing at the moment)**

# Installing Puppet

`apt install build-essential git openssl puppet `

# Configuration

Edit puppet configuration file:

`/etc/puppet/puppet.conf`

```
rpi4:/opt/grin# cat /etc/puppet/puppet.conf 
[main]
server = puppet-pi.grinnode.live 
report = true
certname = ENTER YOUR HOSTNAME HERE (can be any name, no spaces) e.g. RPI4-pi, RPI, myPI00
environment = production
runinterval = 1h
```

# Generating Certificate

*WIP*

Run as root: `puppet agent -t`

# Sending Fingerprint

*WIP*

