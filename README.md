## Safe Internet with Adguard, Unbound and WireGuard - Solution
This solution is a combination of WireGuard, AdGuard, and Unbound in a docker-compose project with the intent of enabling users to quickly and easily create and deploy a personally managed full or split-tunnel WireGuard VPN with ad blocking capabilities , family safe search, parental controls(via AdGuard), and DNS caching with additional privacy options (via Unbound). 

Read the full post at https://naazf.medium.com/safe-internet-with-adguard-unbound-and-wireguard-ee912808c7a8 

If you are after fully automated solution using terraform on Oracle OCI , head to 
https://github.com/fnazz/oracle-freetier-tf-adguard-unbound-wireguard 


## Author
**Naz F**

Docker Compose file contains:
- adguard - https://hub.docker.com/r/adguard/adguardhome
- unbound - https://hub.docker.com/r/mvance/unbound
- wireguard vpn - https://hub.docker.com/r/linuxserver/wireguard

Contains initial unbound.conf as well

## Prerequisites:
- Install docker: https://docs.docker.com/engine/install/
- Install docker-compose: https://docs.docker.com/compose/install/
- Run docker as non-root: https://docs.docker.com/engine/install/linux-postinstall/
- ☁ If using a cloud provider:
    - You need to allow ingress to port `51820`

## Docker Default Setting:
| Container          | IP         |
|--------------------|------------|
| AdGuard Home       | 10.2.0.100 |
| Unbound            | 10.2.0.200 |
| Wireguard IP range | 10.6.0.0/24|

## Quickstart
To get started all you need to do is clone the repository and spin up the containers.

```bash
git clone https://github.com/naazf/docker-adguard-unbound-wireguard.git
cd docker-adguard-unbound-wireguard
docker-compose up -d
```

Run folowing from the host get the QR code:

```bash
ubuntu@adguard-wireguard:~$ sudo docker logs wireguard
wireguard    | **** Internal subnet is set to 10.6.0.0 ****
wireguard    | **** Peer DNS servers will be set to 10.2.0.100 ****
wireguard    | **** No found wg0.conf found (maybe an initial install), generating 1 server and 1 peer/client confs ****
wireguard    | PEER 1 QR code:
wireguard    | █████████████████████████████████████████████████████████████████
wireguard    | █████████████████████████████████████████████████████████████████
wireguard    | ████ ▄▄▄▄▄ █▀▀▀▄ ▀▀▀▀▄█ ██   ▄▀ ██ ██▄▀█    █▄▄█▀ ▄ ██ ▄▄▄▄▄ ████
wireguard    | ████ █   █ █▀▄█▀█▄█▄██▀▄   ▀▀██▀▄█ ▀▄█  ▀ █▀▄█▄ ▄▄▄ ██ █   █ ████
wireguard    | ████ █▄▄▄█ █▀█   ▀▀▄                               ▄██ █▄▄▄█ ████
wireguard    | ████▄▄▄▄▄▄▄█   ▀ ▀   █                         █▄█▄▀ █▄▄▄▄▄▄▄████
wireguard    | ████ ▄▄  █▄▄▄  ▄▀█▀▀▄    ▀█ ▀█  ▄  █▀▀▄▄██▄▄▀▀█▄ ██▀▀ █ █▄█ ▀████
wireguard    | █████  ▄█ ▄  ▀▀█▄▄  █▀ ▀ ▀ ▄  ▄ ▀▄▀▀█ ██ ▀██▀   ▀ ▀▀   ▀  ▀▄ ████
wireguard    | ████▀▀██  ▄▄▄ ██▀▄▄██▀ ██▀▄  ▀▀ █▄█   ▄ ▄█▄██   ▀▄▄█  █▀▀█ ▄▀████
wireguard    | ████ ▄█▀█▀▄▄   ▄███ ▄█ ▀▀▀▀█ ▄█ ▀▀▀▀▀▄ █   █ ███▄ █ ▄▄▄▄▀▀▀ █████
wireguard    | ████▀▄ ▀▀ ▄▄ ▄▄  █▀██    ▀▀▀▀▀  ▄  █▀▀██  ██▀   ▀█▄█▄█  ▄▄▀ ▀████
wireguard    | ████   ▀█ ▄▄                                          █  ▀▀██████
wireguard    | ███████  ▄▄█ █                                        ▄█▀█▀▀▄████
wireguard    | ████ ▄  █▄▄▀  ▄   ▀▄ █ ▄██▀▀█▀   █▄▄█▀▄█▀█▄ █ ▀▄█ ▄█ ▀   █  █████
wireguard    | ████▄██▀█▄▄ ▀ ▄▀                       ▀▄  ▄█ ▀▄  █▀ ▀██▀▄███████
wireguard    | ████ ▀█  ▄▄▄ ██▀███▄█▄█ █▄█▀ ▀ ▄▄▄ ▀▀  ▀▄ ▀▀█   █ █  ▄▄▄   ▄▀████
wireguard    | ████▄██  █▄█  █                                          ▀▀ ▀████
wireguard    | █████▀█▄▄▄▄▄ █▄ ▀▄ ██  ██▀ ▄ █▄ ▄▄▄▀ ▀▄▀█  █▀ █▄ ▄ ▄▄▄  ▄ ▀▄█████
wireguard    | █████▀▄▀  ▄▄█▄▀ ██▄▄▄    █▀  ██    ██ █▄   ██▄ ▄▀█▄██▀▄█   █▀████
wireguard    | ████▄   ▀ ▄ ▀ ▀▀▀▀▀▀█▀██▀ █  █▀█▀███ ▀▄█  █▄ █     ▀▀█▀██▀ ▄█████
wireguard    | ████ ▀ ▄   ██▄ ▀▀▀▄▀█  ▀▀▄ ▄ ▄  █▀▀▄█ ▄█▄▀█▄█▀ ▄▀█▄▀ ▀▀▀ ▀▀ ▀████
wireguard    | ███████ ▄█▄  ▀█▄▄  ▀█ █▀ █▀▄ ▄ ▀▄█▄▄█▀▄█▄▄▄▄█▀ ▀█ █▀  ▄ ██▀▄█████
wireguard    | ████▀█ █▀ ▄                                             █ ▄▀█████
wireguard    | ████▀▄ ▄▄█▄▄  ▄ ▄██▄ ▀ █ ▀ ▄▄█▀▀ ▄ ▀▀▄█▀▄██▀▀ ▄   ▄▄▄▄▀▀▄▀▀▀ ████
wireguard    | ████ ▀▄▄▀▀▄▀▀▀▄ ▄ █▄▄▀ ██▀▄▀ █▄██▀▀▄█▄▄█ ████▄ ▀█▄█▀▄▀ ▀▄ ▀ █████
wireguard    | ████ ▀ ▀▀▄▄ ▄ █▄ ▄ ██ ▄▀█▄▄  ▄ ▄ █▄▀ ▄▄▀██▄▀▀██▀▀▄▄ ▄   ██ ▄▀████
wireguard    | ██████████▄█▀▀█ ▄█ █▄▄ ▀▄▀█▀▀  ▄▄▄ ▀█▀█ ▄▀█▀█▀▀ ██▄▀ ▄▄▄ ▄██▄████
wireguard    | ████ ▄▄▄▄▄ █▄▄▄█▀▄█▀██ ▄ ▀█ ▀  █▄█ ▀▀█▄ ██▄█ ▀▄ ▀█▄▄ █▄█    █████
wireguard    | ████ █   █ █  ▄▄ ▄█   ▄▄█ █▀   ▄ ▄  █ ▄█▄▄█ █▀ ▄████ ▄▄  ▀▀▄▄████
wireguard    | ████ █▄▄▄█ █ ▀ ▄▄█ ▄ ▀▀▄██▄▀█▀█ █▀█▀▀▀▄   ▄ █▀▀▄▀ ▄▀███▀██▀██████
wireguard    | ████▄▄▄▄▄▄▄█▄██▄▄█▄▄▄▄▄██▄█▄▄▄█▄█▄█▄▄▄▄█▄▄▄█████▄▄█▄█▄▄████▄█████
wireguard    | █████████████████████████████████████████████████████████████████
wireguard    | █████████████████████████████████████████████████████████████████
wireguard    | [cont-init.d] 30-config: exited 0.
wireguard    | [cont-init.d] 99-custom-scripts: executing...
wireguard    | [custom-init] no custom files found exiting...
wireguard    | [cont-init.d] 99-custom-scripts: exited 0.
wireguard    | [cont-init.d] done.
wireguard    | [services.d] starting services
```
## Modifying the upstream DNS provider for Unbound
If you choose to not use Cloudflare any reason you are able to modify the upstream DNS provider in `unbound.conf`.

Search for `forward-zone` and modify the IP addresses for your chosen DNS [provider](https://docs.pi-hole.net/guides/dns/upstream-dns-providers/).

>**NOTE:** The anything after `#` is a comment on the line. 
What this means is it is just there to tell you which DNS provider you put there. It is for you to be able to reference later. I recommend updating this if you change your DNS provider from the default values.


```yaml
forward-zone:
        name: "."
        forward-addr: 1.1.1.1@853#cloudflare-dns.com
        forward-addr: 1.0.0.1@853#cloudflare-dns.com
        forward-addr: 2606:4700:4700::1111@853#cloudflare-dns.com
        forward-addr: 2606:4700:4700::1001@853#cloudflare-dns.com
        forward-tls-upstream: yes
```

## Access Adguard Interface (IMPORTANT)
While connected to WireGuard, navigate to http://10.2.0.100:3000 first to setup AdGuard Home before DNS query and adblocking to work.

## Recommended configuration / Split tunnel:
Modify your wireguard client `AllowedIps` to `10.2.0.0/24` to only tunnel the web panel and DNS traffic.

## Wireguard Client Setup:
1. Android: https://serversideup.net/how-to-configure-a-wireguard-android-vpn-client/
2. iOS: https://serversideup.net/how-to-configure-a-wireguard-ios-client/
3. Windows 10: https://serversideup.net/how-to-configure-a-wireguard-windows-10-vpn-client/
4. Linux/Ubuntu: https://tech.serhatteker.com/post/2021-01/how-to-set-up-wireguard-client-on-ubuntu-desktop/
