[![xip-ninja](https://raw.githubusercontent.com/JMousqueton/xip.ninja/master/logo-xip-ninja.png)](#)

[![Build Status](https://travis-ci.org/jmousqueton/xip.ninja.svg?branch=master)](https://travis-ci.org/jmousqueton/xip.ninja)
[![License MIT](https://img.shields.io/badge/license-MIT-lightgrey.svg?style=flat)](https://github.com/jmousqueton/xip.ninja/blob/master/LICENSE)

# xip-ninja

- based on [xip.io](https://github.com/basecamp/xip-pdns)
- Add support for IPv6 record
- Remove Base36
- Add support of dash pattern (you can now resolve 192-168-0-1.xip.ninja)
- Add top-level AAAA Record
- Add MX and TXT record

## Basis
This is a piped backend provider using [PowerDNS](http://powerdns.com/) powering [xip.ninja](https://xip.ninja/).

[xip.ninja](https://xip.ninja/) is a magic domain name that provides wildcard DNS for any IP address.

## Installation

#### :cloud: Install powerdns
```
sudo apt install pdns-server
sudo apt install pdns-backend-pipe
```
### Pull down source
Clone this git repo to somewhere accessible

#### :clipboard: Adjust pdns configuration to use a pipe backend
Open /etc/powerdns/pdns.conf and make these adjustments.

```
launch=pipe
pipe-command=/path/to/xip-pdns/bin/xip-pdns /path/to/xip-pdns/etc/xip-pdns.conf
```

#### :clipboard: Adjust xip-pdns configuration
Rename xip-pdns.conf.example → xip.pdns.conf and make adjustments to the following environment variables:

| Variable | Example | Description |
| --- | --- | --- |
| XIP_DOMAIN | xip.ninja | The root domain of the service |
| XIP_ROOT_ADDRESSES | 51.91.121.80 | The IPv4 addresses returned by an A-record lookup for the root domain |
| XIP_V6_ROOT_ADDRESSES | 2001:41d0:404:200::3632 | The IPv6 addresses returned by an A-record lookup for the root domain |
| XIP_NS_ADDRESSES | 51.91.121.80 | The IP addresses of the nameservers running the xip.ninja container |
| XIP_TIMESTAMP | 2020010912 | SOA serial number |
| XIP_TTL | 3600 | TTL of all responses |
| XIP_MX_RECORDS | "10" "mail.xip.ninja" | The MX records for the domain |
| XIP_TXT_RECORDS | "some text" | the TXT records for the domain |

## :question: Application
This will only respond to dns requests that end in xip.ninja.

Effectively if you ask for 1.2.3.4.xip.ninja it will return 1.2.3.4 as the IP address.

```console
# dig 1.2.3.4.xip.ninja +short
1.2.3.4
```

## :memo: More information

Visit [xip.ninja](https://xip.ninja/).

For 🇫🇷 visit [my blog post](https://www.julienmousqueton.fr/un-enregistrement-dns-sans-nom-de-domaine)


## :+1: Contributors

[//]: contributor-faces

<a href="https://github.com/sstephenson"><img src="https://avatars3.githubusercontent.com/u/2603?s=60&v=4" title="sstephenson" width="80" height="80"></a>
<a href="https://github.com/bn4t"><img src="https://avatars0.githubusercontent.com/u/17193640?s=60&v=4" title="bn4t" width="80" height="80"></a>


[//]: contributor-faces

## :scroll: License

[MIT][license] © [Julien Mousqueton][website]

[license]: https://github.com/JMousqueton/xip.ninja/blob/master/LICENSE
[website]: https://www.julienmousqueton.fr
