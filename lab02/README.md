# Lab 2

## Exercise 2

Below is an example of what your cloud-config file should look like to 
create the etcd cluster:

```
#cloud-config

# You will need to customize the following items in this cloud-config:

# DISCOVERY_URL: replace with the discovery URL you generated in the 
# previous step.

coreos:
  etcd2:
    # generate a new URL for each cluster: https://discovery.etcd.io/new?size=3
    # specify the initial size of your cluster with ?size=X
    discovery: DISCOVERY_URL
    advertise-client-urls: http://$private_ipv4:2379
    initial-advertise-peer-urls: http://$private_ipv4:2380
    # listen on only the official ports
    listen-client-urls: http://$private_ipv4:2379
    listen-peer-urls: http://$private_ipv4:2380
  units:
    - name: etcd2.service
      command: start
```

## Exercise 3

Below is an example of what your cloud-config file should look like after 
adding the mount unit:

```
#cloud-config

# You will need to customize the following items in this cloud-config:

# DISCOVERY_URL: replace with the discovery URL you generated in the 
# previous step.

coreos:
  etcd2:
    # generate a new URL for each cluster: https://discovery.etcd.io/new?size=3
    # specify the initial size of your cluster with ?size=X
    discovery: DISCOVERY_URL
    advertise-client-urls: http://$private_ipv4:2379
    initial-advertise-peer-urls: http://$private_ipv4:2380
    # listen on only the official ports
    listen-client-urls: http://$private_ipv4:2379
    listen-peer-urls: http://$private_ipv4:2380
  units:
    - name: etcd2.service
      command: start
    - name: media-backup.mount
      command: start
      content: |
        [Mount]
        What=/tmp
        Where=/media/backup
        Type=none
        Options=bind
```
