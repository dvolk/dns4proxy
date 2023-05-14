# dns4proxy

This is a DNS server that answers with a round-robin list of proxy ips,
unless the client is in the direct networks list, in which case it
answers with an ip parsed from the hostname.

# Motivation

If you want to access many hosts behind a firewall, you can set up public nginx proxies that have access to the hosts

But if the client is also behind the firewall, you'd prefer to connect directly

In the example below, if you're behind the firewall (direct networks), 1-2-3-4.dynamic.yourdomain.com will return 1.2.3.4

but if you're in front of the firewall, it will return one of the proxies.

You can use nginx to parse the IP from the hostname and proxy the traffic to the correct internal IP

# Configuration example

```
DNS4PROXY_DIRECT_NETWORKS="192.168.0.0/24,192.168.1.0/24"
DNS4PROXY_PROXIES="10.0.0.1,10.0.0.2,10.0.0.3"
DNS4PROXY_DOMAIN_REGEX="^(\d+)-(\d+)-(\d+)-(\d+)\.dynamic\.yourdomain\.com\.$"
```
