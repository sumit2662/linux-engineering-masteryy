# 07 — Linux Networking

## 1. Interfaces and IP addresses
```bash
ip link
ip addr
ip -br addr
```
An interface may be physical, virtual, loopback, or a tunnel.

## 2. Routes and gateway
```bash
ip route
ip route get 1.1.1.1
```
The default route is used when no more specific route matches a destination.

## 3. DNS
```bash
getent hosts example.com
cat /etc/resolv.conf
resolvectl status
```
`getent` uses the system name-service configuration. `resolvectl` is available on systems using systemd-resolved.

## 4. Connectivity
```bash
ping -c 4 1.1.1.1
curl -I https://example.com
traceroute example.com
```
Ping failure does not prove a host is down; ICMP may be filtered. Test the actual application protocol and port.

## 5. Sockets and ports
```bash
ss -tulpen
ss -lnt
ss -tan
```
`-t` TCP, `-u` UDP, `-l` listening, `-n` numeric, `-p` process details. Process information may require elevated privileges.

## 6. Firewall awareness
Ubuntu systems may use UFW; other distributions may use firewalld or nftables.
```bash
sudo ufw status verbose
```
Before enabling a firewall over SSH, ensure the management port is allowed. Otherwise you may lock yourself out.

## Troubleshooting order
1. Interface link state.
2. IP address.
3. Route and gateway.
4. DNS resolution.
5. Service listener.
6. Firewall, proxy, and remote endpoint.

## Lab
Run `ip -br addr`, `ip route`, `getent hosts example.com`, and `curl -I https://example.com`. Record which layer succeeds or fails.
