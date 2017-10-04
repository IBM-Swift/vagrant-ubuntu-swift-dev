# vagrant-ubuntu-swift-dev

> Note: this repository is designed to help you *contribute to the Swift project itself*. If you just want to develop in Swift, use [Apple's snapshots](https://swift.org/download/).

This repository provides a `Vagrantfile` which will automatically provision and configure an Ubuntu 14.04 Swift development environment.

It will:

1. Install an Ubuntu 14.04 virtual machine
2. Install development prerequisites
3. Clone the latest Swift source code from GitHub
4. Clone all dependent source repositories

# Prerequisites
1. [git](https://git-scm.com)
2. [Vagrant](https://www.vagrantup.com)
3. [Virtualbox](https://www.virtualbox.org)

# Usage Guide

```
$ git clone https://github.com/IBM-Swift/vagrant-ubuntu-swift-dev.git
$ cd vagrant-ubuntu-swift-dev
$ vagrant up
```

Once your VM has been provisioned, you can connect to it using the `vagrant ssh` command.

# Building Swift

See [Building Swift](https://github.com/apple/swift#building-swift).
