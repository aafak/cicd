```
aafak@aafak-virtual-machine:~$ minikube start --driver=docker
* minikube v1.32.0 on Ubuntu 22.04
* minikube 1.33.1 is available! Download it: https://github.com/kubernetes/minikube/releases/tag/v1.33.1
* To disable this notice, run: 'minikube config set WantUpdateNotification false'

* Using the docker driver based on existing profile
* Starting control plane node minikube in cluster minikube
* Pulling base image ...
* Restarting existing docker container for "minikube" ...
* Preparing Kubernetes v1.28.3 on Docker 24.0.7 ...
* Configuring bridge CNI (Container Networking Interface) ...
* Verifying Kubernetes components...
  - Using image docker.io/kubernetesui/dashboard:v2.7.0
  - Using image docker.io/kubernetesui/metrics-scraper:v1.0.8
  - Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
  - Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
  - Using image registry.k8s.io/ingress-nginx/controller:v1.9.4
  - Using image gcr.io/k8s-minikube/storage-provisioner:v5
* Verifying ingress addon...
* Some dashboard features require the metrics-server addon. To enable all features please run:

        minikube addons enable metrics-server


* Enabled addons: storage-provisioner, ingress, default-storageclass, dashboard
* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default


aafak@aafak-virtual-machine:~$ minikube addons enable metrics-server
* metrics-server is an addon maintained by Kubernetes. For any concerns contact minikube on GitHub.
You can view the list of minikube maintainers at: https://github.com/kubernetes/minikube/blob/master/OWNERS
  - Using image registry.k8s.io/metrics-server/metrics-server:v0.6.4
* The 'metrics-server' addon is enabled
aafak@aafak-virtual-machine:~$
```


aafak@aafak-virtual-machine:~$ minikube dashboard --url
* Verifying dashboard health ...

* Launching proxy ...

* Verifying proxy health ...
http://127.0.0.1:39367/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/



*****************************From remote access:
```
aafak@aafak-virtual-machine:~$ ip address
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:33:78:23 brd ff:ff:ff:ff:ff:ff
    altname enp2s1
    inet 192.168.203.128/24 brd 192.168.203.255 scope global dynamic noprefixroute ens33
       valid_lft 1209sec preferred_lft 1209sec
    inet6 fe80::690a:a290:9d86:f7c2/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:31:9a:08:66 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
4: br-3ebe9952fd2c: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:de:05:1c:e3 brd ff:ff:ff:ff:ff:ff
    inet 172.18.0.1/16 brd 172.18.255.255 scope global br-3ebe9952fd2c
       valid_lft forever preferred_lft forever
5: br-d631a5a76bf7: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:7a:d8:da:f6 brd ff:ff:ff:ff:ff:ff
    inet 192.168.49.1/24 brd 192.168.49.255 scope global br-d631a5a76bf7
       valid_lft forever preferred_lft forever
    inet6 fe80::42:7aff:fed8:daf6/64 scope link
       valid_lft forever preferred_lft forever
7: veth2b26940@if6: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br-d631a5a76bf7 state UP group default
    link/ether ba:f3:54:81:8d:dd brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet6 fe80::b8f3:54ff:fe81:8ddd/64 scope link
       valid_lft forever preferred_lft forever
aafak@aafak-virtual-machine:~$

aafak@aafak-virtual-machine:~$ sudo ufw status
[sudo] password for aafak:
Status: inactive
aafak@aafak-virtual-machine:~$ sudo ufw allow 39367
Rules updated
Rules updated (v6)
aafak@aafak-virtual-machine:~$ sudo ufw status
Status: inactive
aafak@aafak-virtual-machine:~$ sudo ufw allow http
Rules updated
Rules updated (v6)
aafak@aafak-virtual-machine:~$ sudo ufw allow https
Rules updated
Rules updated (v6)
aafak@aafak-virtual-machine:~$ sudo ufw status
Status: inactive
aafak@aafak-virtual-machine:~$ sudo ufw statussudo ufw default allow outgoing
^C
aafak@aafak-virtual-machine:~$ sudo ufw default allow outgoing
Default outgoing policy changed to 'allow'
(be sure to update your rules accordingly)
aafak@aafak-virtual-machine:~$ sudo ufw default allow incoming
Default incoming policy changed to 'allow'
(be sure to update your rules accordingly)
aafak@aafak-virtual-machine:~$ sudo ufw status
Status: inactive
aafak@aafak-virtual-machine:~$ sudo ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)?
Aborted
aafak@aafak-virtual-machine:~$ sudo ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
aafak@aafak-virtual-machine:~$ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
5432/tcp                   ALLOW       Anywhere
39367                      ALLOW       Anywhere
80/tcp                     ALLOW       Anywhere
443                        ALLOW       Anywhere
5432/tcp (v6)              ALLOW       Anywhere (v6)
39367 (v6)                 ALLOW       Anywhere (v6)
80/tcp (v6)                ALLOW       Anywhere (v6)
443 (v6)                   ALLOW       Anywhere (v6)

aafak@aafak-virtual-machine:~$ kubectl proxy --address='0.0.0.0' --disable-filter=true
W0721 10:17:21.573103   34158 proxy.go:177] Request filter disabled, your proxy is vulnerable to XSRF attacks, please be cautious
Starting to serve on [::]:8001
```

http://192.168.203.128:8001/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/workloads?namespace=default