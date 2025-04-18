# Introduction

This project explores using [`libvirt`](https://libvirt.org/) based tools to create [QEMU/KVM](https://www.youtube.com/watch?v=BgZHbCDFODk) Virtual Machine (*VM*) with workflow inspired by [Vagrant](https://en.wikipedia.org/wiki/Vagrant_(software)).

Intention is to create VM from cloud disk image provided by GNU/Linux distribution and for basic initialization use [`cloud-init`](https://cloudinit.readthedocs.io/en/latest/).

> [!NOTE]
> The project is developed on [Debian 12](https://www.debian.org/) if you use another distribution have that in mind if something doesn't work as expected.

🦈

# Requirements

- GNU/Linux OS capable of running QEMU/KVM based VMs.

# Design goals

- Simple and easy to adapt.
- Practice [suckless.org philosophy](https://suckless.org/philosophy/), if possible.
- Support basic workflow, for everything else there is [Vagrant](https://en.wikipedia.org/wiki/Vagrant_(software)).
- Minimal third party dependencies.
- No compiler.

# Installation and setup

## QEMU and Virtual Machine Manager

Check compatibility:

    grep -o 'vmx\|svm' /proc/cpuinfo # If nothing comes back check BIOS to make sure virtualization is enabled

Install and setup on Debian/Ubuntu:

    sudo apt-get install virt-manager
    sudo adduser <USER_NAME> libvirt # Add user to `libvirt` group
    sudo adduser <USER_NAME> libvirt-qemu

[Video instructions](https://www.youtube.com/watch?v=ozYKkaVK0_A). 📽️

## Cloud disk image

Download [Debian `genericcloud` image](https://cdimage.debian.org/images/cloud/) for version you wish to use in VM. E.g. [https://cdimage.debian.org/images/cloud/bookworm/20241004-1890/debian-12-genericcloud-amd64-20241004-1890.qcow2](https://cdimage.debian.org/images/cloud/bookworm/20241004-1890/debian-12-genericcloud-amd64-20241004-1890.qcow2).

You can also use cloud image for another distribution if you wish.

## 🦈 installation

Copy [`./shark`](shark), after reviewing the code, to your `echo $PATH` and set execute permission on it with:

    chmod +x shark

# Usage

To create VM config files, most notably `Sharkfile` which defines VM, in empty directory execute:

    shark init

[`./example_vm_configuration_generated_with_init_action`](example_vm_configuration_generated_with_init_action) directory contains example of VM configuration generated with `shark init` command.

You **must** edit `Sharkfile` and `user-data` before creating VM with command:

    shark up

To shutdown VM:

    shark down

To destroy VM and its storage:

    shark destroy

# FAQ

## What are alternatives to this project?

- [Vagrant](https://en.wikipedia.org/wiki/Vagrant_(software))
