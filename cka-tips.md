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

If a tempate from docs.kubernetes is required (e.g. persistent volume), try curling the yaml link in the web document:
`curl -LO https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/pods/storage/pv-volume.yaml`

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

* there may be changes to the api, especially during configuration for coredns - use `apps/v1` for `kind: Deployment` instead of `extensions/v1beta1`

* e2e test issue workaround: https://github.com/kubernetes/test-infra/issues/14712

* if port-forward issues are seen after OSX Catalina upgrade or VMware Fusion upgrade, e.g.

```
Vagrant failed to apply the requested port forward. The following
error message was generated while attempting to apply the port
forward rule:

  Port forward conflict on host port 2730
```
try cleaning up the [vagrant-vmware](https://github.com/hashicorp/vagrant/issues/10575#issuecomment-517168661) NAT settings.

## Other Tips

Interesting study guides:
[David-VTUK](https://github.com/David-VTUK/CKA-StudyGuide)
[stretchcloud](https://github.com/stretchcloud/cka-lab-practice)
[CKAD](https://github.com/dgkanatsios/CKAD-exercises)

