# Local DNS Resolution over TLS

This repo provides a dockerized dns resolution system with hooks for private hosted DNS support and outbound DNS encryption over TLS. It is desigend to work on ARM hardware as I run this on two Raspberry Pi 3 systems for my home network.

## To Use

1. Clone Repo
2. Copy `.env.example` to `.env`
3. Edit `.env` as needed
4. Edit `config/dnsmasq.conf` if needed
5. Add any extra config under `config/dnsmasq.d/` - I recommend one file per domain to keep things organized. 
6. Do a `docker-compose up -d` on the command line and enjoy local DNS. 

## Thanks

Special thanks to 

[Anže Valher](https://github.com/anzevalher) for the base image.

<img height="20" width="20" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/docker.svg" /> [anzevalher/dnsmasq](https://hub.docker.com/r/anzevalher/dnsmasq)

<img height="20" width="20" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/github.svg" /> [anzevalher/dnsmasq](https://github.com/anzevalher/dnsmasq)

[iurimieras](https://hub.docker.com/u/iurimieras) for the stubby image

<img height="20" width="20" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/docker.svg" /> [iurimieras/stubby_armv7](https://hub.docker.com/r/iurimieras/stubby_armv7)

## Notes / TODO

* This uses a bit of a network hack to get around DNSMasq not accepting the service name as a forwarding DNS server. It isn't scalable as a result. This is ok for its intended use, but user beware. 
* The stubby image is old. It should probably be upgraded. If I can find the original repo I'll see about a PR. Otherwise I will likely have to make my own or find an alternative. 
* I plan on investigating unbound. DNSMasq is a great lightweight solution, but it is hacky from a DNS perspective.
* [Matthew Vance](https://github.com/MatthewVance/stubby-docker) has a great solution for non-arm hardware. Maybe I can use that as a base.
* Maybe PiHole is the better option in general. I will have to investigate that first.
