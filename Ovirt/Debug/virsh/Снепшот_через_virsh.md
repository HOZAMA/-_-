# Как создать моментальный снимок виртуальной машины KVM с помощью команды virsh

* <https://www.linuxtechi.com/create-revert-delete-kvm-virtual-machine-snapshot-virsh-command/>

## Просмотрим список вм на ноде, для того чтоб невводить пароль используем ключ -r
```console
virsh -r list --all
```
#№ Создаем снепшот
```console
virsh snapshot-list <VM_NAME>
```

# Мы можем просмотреть размер снепшота, используя приведенную ниже команду qemu-img

```console
qemu-img info /var/lib/libvirt/images/snaptestvm.img
```
