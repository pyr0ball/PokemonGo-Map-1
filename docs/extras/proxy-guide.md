Using Proxies with PokemonGo-Map
===================

Disclaimer: **This guide is only a framework for individual use. Implementation on large scale is not supported**

Part 1: Finding Usable Proxies
------------------------------

First things first, you'll want to find some usable proxies. There are free public proxies available, however most of these are already blocked from Niantic's servers. A better option is to use a private proxy or proxy list service. 

[ProxyBliss](http://proxybliss.com/proxy-packages/ "ProxyBliss")

[Free Proxies](http://lmgtfy.com/?q=free+proxies "Free Proxies")

Part 2: Universal Method - Using Server Configuration
-----------------------------------------------------

The easiest and simplest method for using proxies with your map is to use the built-in configuration, however this is limited to using only one proxy at a time. You can accomplish this one of two ways, either by adding the proxy to your config.ini, or using it on the command line.

###Using the Configuration File:

Find the "Misc" section in config.ini and edit the proxy line thusly:

```
# Misc
#gmaps-key:                       # your Google Maps API key
proxy: socks5://127.0.0.1:9050    # Proxy URL e.g. socks5://127.0.0.1:9050
#webhook:                         # webhook URL (including http://)
#webhook-updates-only:            # only send updates to webhooks, (excludes gyms & non-lured pokéstops)
```

###Using the Command Line Switch:

Add the `-px` argument to your launch script:

```
python runserver.py -px socks5://127.0.0.1:9050
```

Part 3: Linux Server - Using Proxychains-NG
-------------------------------------------

**Note. proxychains-ng is not available from package repositories. The package "proxychains" that can be installed using apt and yum, is outdated and broken, and lacks the ability to whitelist local connections which are required for your map to connect to it's database. Please follow the instructions below for installation**

###Step 1. - Install proxychains-ng

```
sudo apt-get update
sudo apt-get install build-essential
git clone https://github.com/rofl0r/proxychains-ng.git
cd proxychains-ng
./configure --prefix=/usr --sysconfdir=/etc
make
make install
make install-config
```

###Step 2. - Configure proxychains-ng
