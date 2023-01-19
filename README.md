# Kube-VIP with DHCP LoadBalancers

```yaml
apiVersion: fleet.cattle.io/v1alpha1
kind: GitRepo
metadata:
  name: dgiebert-fleet-kubevip
  namespace: fleet-default
spec:
  branch: main
  repo: https://github.com/dgiebert/fleet-kubevip.git
```

## Requirements
- **Disable the servicelb for k3s**
- Uses the default network interface (autodetected)
- Tested with Harvester VMs only (but should work on all nodes)

## How it works

> In order to do this, we need to signify to kube-vip and the cloud provider that we don't need one of their managed addresses. 
> We do this by explicitly exposing a Service on the address 0.0.0.0. When kube-vip sees a Service on this address, it will create 
> a macvlan interface on the host and request a DHCP address. Once this address is provided, it will assign it as the LoadBalancer 
> IP and update the Kubernetes Service.
>
> -- <cite>[Kubevip Docs][1]</cite>

[1]: https://kube-vip.io/docs/usage/kubernetes-services/?query=dhcp#using-dhcp-for-load-balancers-experimental-kube-vip-v021

1. Set the `global-cidr` in the `kubevip` configmap to be `0.0.0.0/32` this will assign all LBs the IP `0.0.0.0` done by the kube-vip-cloud-provider
2. The `kube-vip` pod will look for services that are configured this and request a DHCP address 

### Links
- https://kube-vip.io/docs/usage/k3s/#step-5-service-load-balancing
- https://github.com/kube-vip/kube-vip-cloud-provider#create-an-ip-pool-using-a-cidr
- https://github.com/kube-vip/kube-vip-cloud-provider#ip-address-functionality