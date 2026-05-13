# OpenShift Local (crc)

OpenShift Local on RHEL 9.7 (installation is not currently working on RHEL 10.0)

## SSH Access
```bash
ssh-keygen -t rsa
ssh-copy-id -i /home/jpastor/.ssh/id_rsa_4sshAuth.pub jpastor@192.168.1.62
```

## Download CRC
```bash
wget https://developers.redhat.com/content-gateway/rest/mirror/pub/openshift-v4/clients/crc/latest/crc-linux-amd64.tar.xz
tar -xvf crc-linux-amd64.tar.xz
mv crc ~/bin
```

## Install
```bash
crc delete # Remove previous cluster (if present)
crc config set preset openshift # Configure to use openshift preset
crc config set disk-size 100 # Incredisk from 30G to 100G
crc setup # Initialize environment for cluster
crc start # Start the cluster
```

## Config Network Access

```bash
sudo firewall-cmd --zone=public --add-service=http --permanent
sudo firewall-cmd --zone=public --add-service=https --permanent
sudo firewall-cmd --reload
```



## Doc

https://crc.dev/docs/using/

