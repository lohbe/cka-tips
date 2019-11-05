# CKA Tips

## CKA Syllabus

Read the official CKA certification [page](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/) especially for:

* candidate handbook
* curriculum

## Vim & bash preferences

`:autocmd FileType yaml setlocal ai ts=2 sw=2 et nu rnu` 

## Browser preferences

* add Chrome search engine to speed up searches.

## Mummshad's Kubernetes the hard way

* VMware Fusion can be used - the `Vagrantfile` in this repo has been extended to use it: `vagrant up --provider=vmware_fusion`.

* For some reason, it was configured that the load balancer VM's hostname is `loadbalancer`. It is however, not pingable - the `/etc/hosts` file shows the host `lb` instead.

* `enp0s8` may not be available with some configurations, especially in VMware fusion: `ip addr` should show the correct interface of internal range 192.x instead - e.g. `eth1`.

* kubelet will not start with swap error in /var/log/syslog. remember to turn off swap in worker nodes via:
```bash
sudo sed -i.bak '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
sudo swapoff -a
```

* e2e test issue workaround: https://github.com/kubernetes/test-infra/issues/14712

