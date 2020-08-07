# Local DNS Resolution over TLS

This repo provides a dockerized dns resolution system based on [PiHole](https://github.com/pi-hole/docker-pi-hole) with outbound DNS encryption over TLS via [stubby](https://github.com/getdnsapi/stubby) and [Cloudflare](https://www.cloudflare.com/learning/dns/dns-over-tls/) (configurable). It is desigend to work on ARM hardware as I run this on two Raspberry Pi 3 systems for my home network.

## To Use

1. Clone Repo
2. Copy `.env.example` to `.env`
3. Edit `.env` as needed
5. Add any extra config under `config/dnsmasq.d/` - I recommend one file per domain to keep things organized. PiHole will serve these files as normal. Note: Do *not* name the file 01-pihole.conf. That will be overwritten. Certain config options will not be avaiable as pihole uses them. An example would be cache settings.
6. Do a `docker-compose up -d` on the command line and enjoy local, safe DNS with ad-blocking! 

## Thanks

Special thanks to 

* The [PiHole](https://github.com/pi-hole/docker-pi-hole) team and community
* [iurimieras](https://hub.docker.com/u/iurimieras) for the stubby image [iurimieras/stubby_armv7](https://hub.docker.com/r/iurimieras/stubby_armv7)
* [Vincent Composieux](https://github.com/eko/) for the prometheus metrics exporter [ekofr/pihole-exporter](https://hub.docker.com/r/ekofr/pihole-exporter)

## Notes

* This uses a bit of a network hack to get around DNSMasq not accepting the service name as a forwarding DNS server. It isn't scalable as a result. This is ok for its intended use, but user beware. 
* PiHole is the better option for adblocking currently.
  * PiHole is an interesting beast. It uses a custom DNSMasq version under the hood.
  * It is not great. The container behaves oddly. For example, it reports as running/healthy even though it is still loading and, despite having a config directory it seems to overwrite the config on every load.

## TODO

* Need to build my own stubby container to allow low-priviledged port binds and clean a lot of things up.
  * `setcap CAP_NET_BIND_SERVICE=+eip /opt/stubby/bin/stubby`
  * Base off of Matthew Vances stubby build [here](https://github.com/MatthewVance/stubby-docker/blob/master/stubby/Dockerfile)
