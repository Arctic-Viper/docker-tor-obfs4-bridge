# Forked by Arc :D

# docker: tor obfs4 bridge 🐳
Tor bridge running obfs4 obfuscation protocol via
[lyrebird](https://gitlab.torproject.org/tpo/anti-censorship/pluggable-transports/lyrebird) on Alpine

Alpine port of https://dip.torproject.org/torproject/anti-censorship/docker-obfs4-bridge

## usage

`$OR_PORT` and `$PT_PORT` can be random but must match docker

(see `/proc/sys/net/ipv4/ip_local_port_range` for range)

```sh
docker run --name tor_obfs4_bridge \
    -e OR_PORT=42218 -p 42218:42218 \
    -e PT_PORT=51804 -p 51804:51804 \
    -e CONTACT_INFO=admin@optional.com \
    -e NICKNAME=nickname \
    fphammerle/tor-obfs4-bridge
```

add `-v tor_obfs4_bridge_data:/var/lib/tor` to keep server's identity key
when restarting the container

additionally add `--read-only --tmpfs /tmp:rw,size=4k`
to make the container's root filesystem read only

verify status of bridge at https://metrics.torproject.org/rs.html

## further reading

https://community.torproject.org/relay/setup/bridge/
