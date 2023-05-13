Wordpress for Kubernetes with PersistentVolume
-----------------------------------------------

NFS file share /mnt/nfs_share/wp_project has to be created before all steps.
--------------

sudo apt update

sudo apt list --upgradable

sudo apt upgrade


ON SERVER
---------
sudo apt install nfs-kernel-server

sudo mkdir -p /mnt/nfs_share

sudo chmod 777 /mnt/nfs_share

sudo echo "/mnt/nfs_share 10.1.6.175/32(rw,sync,no_subtree_check,no_root_squash) " >> /etc/exports

sudo exportfs -a


ON CLIENT (in this case 10.1.6.175)
----------------------------------
sudo apt install nfs-common

sudo mkdir -p /mnt/nfs_share

sudo mount 10.1.6.173:/mnt/nfs_share /mnt/nfs_share 


or add to /etc/fstab for auto mount

sudo echo "10.1.6.173:/mnt/nfs_share /mnt/nfs_share  nfs      defaults    0       0" >> /etc/fstab

sudo mount -a



0. Allow access to NFS share:

sudo mkdir /mnt/nfs_share/wp_project

sudo chmod -R  777 /mnt/nfs_share/wp_project

it will put Wordpress files to /mnt/nfs_share/wp_project/wp  and MySQL database to /mnt/nfs_share/wp_project/mysql


1. You can deploy everything through kustomization.yaml file using: 

kubectl apply -k .



References:

1) https://gitlab.com/nb-tech-support/devops/-/blob/master/Deploy%20MySQL%20on%20Kubernetes
2) https://medium.com/@madushagunasekara/export-mysql-db-dump-from-kubernetes-pod-and-restore-mysql-db-on-kubernetes-pod-6f4ecc6b5a64
