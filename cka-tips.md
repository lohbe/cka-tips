# CKA Tips

## CKA Syllabus

Read this.
https://github.com/cncf/curriculum/blob/master/certified_kubernetes_administrator_exam_v1.15.pdf

## Vim & bash preferences

`:autocmd FileType yaml setlocal ai ts=2 sw=2 et nu rnu` 

## Browser preferences

* add Chrome search engine to speed up searches.

## Mummshad's Kubernetes the hard way

* for some reason, it was configured that the load balancer VM's hostname is `loadbalancer`. It is however, not pingable - the `/etc/hosts` file shows the host `lb` instead.

* `enp0s8` may not be available with some configurations, especially in VMware fusion: `ip addr` should show the correct interface of internal range 192.x instead - e.g. `eth1`

* kubelet will not start with swap error in /var/log/syslog

remember to turn off swap in worker nodes via:
```bash
sudo sed -i.bak '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab`
sudo swapoff -a
```

e2e test issue workaround: https://github.com/kubernetes/test-infra/issues/14712
