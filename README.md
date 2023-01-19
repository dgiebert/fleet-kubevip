# Kube-VIP with DHCP LoadBalancers

## Requirements
- **Disable the servicelb for k3s**
- Uses the default network interface (autodetected)
- Tested with Harvester VMs only (but should work on all nodes)


### Sources
- https://kube-vip.io/docs/usage/kubernetes-services/?query=dhcp#using-dhcp-for-load-balancers-experimental-kube-vip-v021
- https://kube-vip.io/docs/usage/k3s/#step-5-service-load-balancing
- https://github.com/kube-vip/kube-vip-cloud-provider#create-an-ip-pool-using-a-cidr
- https://github.com/kube-vip/kube-vip-cloud-provider#ip-address-functionality