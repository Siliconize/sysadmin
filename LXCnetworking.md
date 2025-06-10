# LXC Networking

## Bridges 
Bridges are used ot connect VMs to a network.

> **Bridges**: Sort of like a software switch \
> They are a basic function of the linux kernel and are ussuallz created with the bridge-utils package

There are two types of bridges you can configure:
- **Host Bridge**: vms/ containers are directly connected ot the host network and appear like any other physical machne on the network
- **NAT**: Subnet is created within the Host with **private** IPs for the containers, this is a NAT bridge.


### Bridged Mode
Bridges containers to host's physical interface, like the 'eth0' interface. 

This type of bridge has the same layer 2 network as the host.

The container will also get an ip from the home routers dhcp. Makes sense because the Host isn't running a DHCP server.

> Now the question for my project is: What would I use to bridge the host and the container to simulate real world 

A sample /etc/network/interfaces config for a bridge: 
```bash
auto br0
iface br0 inet dhcp
bridge_ports eth0
bridge_stp off
bridge_fd 0
bridge_maxwait 0
```

Now you can set static ips either using the home router and doing a dhcp lease using the mac addresses of the container, or just using the containers network settings.

### NAT
> I think a NAT might be what I should use for my lab setup

A NAT exists as a private subnet, it is not bridged to the Hosts eth0

It creates a private network within the hosts computer with the container getting a private ip.

LXC ships with a NAT bridge by default called "lxcbr0".

Setup by the "lxc-net script"



## Sources
https://archives.flockport.com/flockport-labs-use-lxc-containers-as-routers/
https://archives.flockport.com/lxc-networking-guide/