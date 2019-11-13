# CKA Tips

## CKA Syllabus

Read the official CKA certification [page](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/) especially for:

* candidate handbook
* curriculum

## Vim & bash preferences

`:autocmd FileType yaml setlocal ai ts=2 sw=2 et nu rnu` 

also useful in some situations:

```bash
:syntax on
:set syntax=whitespace
```

For Macbook Pro users with touch-bar, it can be useful to map the Caps lock key to ESC.

## Browser preferences

Add Chrome search engine to speed up searches. Go to Settings | Manage search Engines to add a search engine. I use:

* Keyword k, URL https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#%s
* Keyword kio, URL https://kubernetes.io/docs/search/?q=%s
* Keyword kapi, URL https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.16/#%s

## Imperative management

Use `kubectl create` or `run` to create and modify objects as opposed to declarative `apply` - it is much faster.

In some cases, reference existing objects via config files, or `kubectl get -o yaml` to create new ones. e.g. Daemonsets, new kube-scheduler, etc.

For application lifecycle management, use both `kubectl set` or `edit`.

Speed up deletions by using `--grace-period=1`

## OpenSSL

To view certificate info:

`openssl x509 -in $INFILE -text -noout`

(Not tested) To sign new certificate, pass the CSR and CA pair:

```bash
openssl x509 req -in $CSR \
-CA $CACERT
-CAkey $CAkey
-CAcreateserial
-out $NEWCERT
```

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

## Other Tips

Interesting Study [Guide](https://github.com/David-VTUK/CKA-StudyGuide)

