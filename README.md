Ansible role `pxeboot`
=========

Ansible role that installs and configures a PXE Boot server.

Requirements
------------

None.

Role Variables
--------------

|      Variable       | Default |                                       Comment                                       |
| :------------------ | :------ | :---------------------------------------------------------------------------------- |
| pxeboot_ip          | -       | The IP address of the PXEboot server.                                               |
| pxeboot_images      | []      | List of PXEboot images to install on the clients.                                   |
| pxeboot_dhcp        | false   | Sets PXEboot server up as DHCP server. Default uses virtualbox dhcpd.conf settings. |
| pxeboot_dhcp_config | -       | Loads local dhcpd.conf file. (See `Using local files` section)                      |


Options for `pxeboot_images` variable:

|     Option      |          Required           |                            Comment                            |
| :-------------- | :-------------------------- | :------------------------------------------------------------ |
| name            | yes                         | Name of the image OS.                                         |
| kernel_url      | yes (if local not supplied) | Link to image kernel file using http, https or ftp.           |
| initrd_url      | yes (if local not supplied) | Link to image initrd file using http, https or ftp.           |
| liveos_url      | yes (if local not supplied) | Link to image LiveOS file using http, https or ftp.           |
| kickstart_url   | no                          | Link to image kickstart file using http, https or ftp.        |
| local_kernel    | yes (if url not supplied)   | Loads local kernel file. (See `Using local files` section)    |
| local_initrd    | yes (if url not supplied)   | Loads local initrd file. (See `Using local files` section)    |
| local_liveos    | yes (if url not supplied)   | Loads local LiveOS file. (See `Using local files` section)    |
| local_kickstart | no                          | Loads local kickstart file. (See `Using local files` section) |


Using local files
-----------------

To use the `local_*` variables, the files have to be places in a subfolder called "files" within this ansible role. The directory structure should look like this:

```
.
├── defaults
│   └── main.yml
├── files
│   ├── centos.cfg
│   ├── dhcpd.conf
│   └── fedora.cfg
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── README.md
├── tasks
│   └── main.yml
├── tests
│   ├── inventory
│   └── test.yml
└── vars
    └── main.yml
```

Dependencies
------------

None.

Example Playbook
----------------

```
pxeboot_ip: 172.16.0.3

pxeboot_images:
  - name: "Centos"
    kernel_url: "http://ftp.belnet.be/mirror/ftp.centos.org/7/os/x86_64/isolinux/vmlinuz"
    initrd_url: "http://ftp.belnet.be/mirror/ftp.centos.org/7/os/x86_64/isolinux/initrd.img"
    liveos_url:  "http://ftp.belnet.be/mirror/ftp.centos.org/7/os/x86_64/LiveOS/squashfs.img"
    local_kickstart: centos.cfg

  - name: "Fedora"
    kernel_url: "http://ftp.halifax.rwth-aachen.de/fedora/linux/releases/28/Workstation/x86_64/os/isolinux/vmlinuz"
    initrd_url: "http://ftp.halifax.rwth-aachen.de/fedora/linux/releases/28/Workstation/x86_64/os/isolinux/initrd.img"
    liveos_url:  "http://ftp.halifax.rwth-aachen.de/fedora/linux/releases/28/Workstation/x86_64/os/images/install.img"
    local_kickstart: fedora.cfg
```

License
-------

BSD

Author Information
------------------

[Niel De Boever](https://github.com/NielDB)
