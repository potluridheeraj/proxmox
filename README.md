# proxmox
This is a repo where I create proxmox homer server details 


virt-customize -a jammy-server-cloudimg-amd64.img --install qemu-guest-agent

virt-customize -a jammy-server-cloudimg-amd64.img --run-command "sudo truncate -s 0 /etc/machine-id /var/lib/dbus/machine-id"

qemu-img resize jammy-server-cloudimg-amd64.img +2G

qm create 6400 --memory 2048 --core 2 --name ubuntu-cloud --net0 virtio,bridge=vmbr0

qm importdisk 6400 jammy-server-cloudimg-amd64.img local-lvm

qm set 6400 --scsihw virtio-scsi-pci --scsi0 local-lvm:vm-6400-disk-0

qm set 6400 --ide2 local-lvm:cloudinit

qm set 6400 --boot c --bootdisk scsi0

qm set 6400 --serial0 socket --vga serial0

qm set 6400 --agent 1,fstrim_cloned_disks=1


