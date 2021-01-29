# pi-hole-compose

Pi-hole simplified in `<=` 3 sentences:

> Computers use DNS to find the IP address that belongs to a domain name, e.g. the IP address for `google.com`.
> Computers can't load content without knowing the IP address. 
> Pi-hole is a DNS server that prevents your computer finding out the IP address for content you don't want loaded (e.g. adverts) or sent (e.g. tracking analytics) 

This project is based on https://github.com/pi-hole/docker-pi-hole with everything stripped out bar the docker-compose file.
This is the config I use for Pi-hole on a Pi4. I use Pi-hole to **block distracting websites** too. 
If you find it useful, please consider donating to [Pi-hole](https://pi-hole.net/donate/). 

## Requirements

* a Pi (or other machine) to run your Pi-hole
* [docker](https://docs.docker.com/engine/install/debian/#install-using-the-convenience-script) and [docker-compose](https://docs.docker.com/compose/install/) installed on said machine
* a router that allows you to configure DNS, or, failing that, a device you use for viewing web sites (e.g. mobile phone) that allows you to configure DNS
* you'll need to know the IP address of the machine running your Pi-hole. You need to use that IP address in the DNS config of your router or device.

## Passwords

There are some options to set a password

1. Do nothing but `docker-compose up`. The admin password used is in [.env](.env). Not recommended.
2. Change the [.env](.env) file and `docker-compose up`. Remember not to commit your altered `.env` file.
3. Bring up the stack like `WEB_PASSWORD=letmein2 docker-compose up`.
4. Like 3, but `export WEB_PASSWORD=letmein2; docker-compose up`.

You can log into admin console on `http://localhost/admin/index.php?login` if you're running it locally. 

You can start up Pi-hole with a new password, but first 
you must

* `docker-compose down`
* open `etc-pihole/setupVars.conf` and remove the line containing 
`WEBPASSWORD=<some-password-hash>`,
* then bring up the stack `docker-compose up -d` (`d` to run in detached/background)

## Starting, stopping, updating

If you're not familiar with docker-compose, the following commands may be useful:

```
# from the folder than contains your docker-compose.yml file
# starting Pi-hole in background
docker-compose up -d
# stopping
docker-compose down
# updating and starting
docker-compose pull && docker-compose up
```