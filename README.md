# Development machine for `smtrat` & `carl`

Setting up a development-environment for [carl](https://github.com/smtrat/carl) and [smtrat](https://github.com/smtrat/smtrat) can be a tedious process. This Vagrant-machine therefore includes all required and (non graphical) optional dependencies to build and run the projects. However, there is only the `gcc`-compiler included, `clang` is not available. The machine is based `Ubuntu 16.04.* LTS`. 

## Requirements

Obviously, you need to have [vagrant](https://www.vagrantup.com/) and some provisioner (e.g. [VirtualBox](https://www.virtualbox.org/)) installed.

You can then either download the raw `Vagrantfile` and put it in a directory of your choice or you can `git clone` this repository.

## Runngin the machine

From the directory that holds the `Vagrantfile` run `vagrant up`.

**Note:** If you're using Windows as your host-system then you must run `vagrant up` from a shell with admin-permissionis, otherwise you will face a "protocol-error". This is because `carl` works with symlinks and these are otherwise disabled on windows-hosts for shared folders.

You can then ssh into the machine with `vagrant ssh`.

## Building

Because `carl` is a dependency of `smtrat` you must build the projects in order.

The VM automatically clones the repository from GitHub to `/vagrant/carl` and `/vagrant/smtrat` respectively.

Note, that the `/vagrant`-directory is automatically shared with your host-system. On your host-system you'll find the shared folder wherever you put your `Vagrantfile`.

To build `carl`:
```
cd /vargrant/carl
rm -R build && mkdir build && cd build
cmake ../
make
make test doc
```

To build `smtrat`:
```
cd /vagrant/smtrat
mkdir build && cd build
cmake ../
make
```

## Known issues and planned features

* I want to include remote-debugging capabilities. This is why the virtual machine already connects to your private network. It is reachable from your host-system under the static ip-address `192.168.33.10`.
* There is still an issue with building the documentation for `carl` that wants to be adressed.
* `smtrat` ships with a GUI. However, it requires additional optional dependencies that are currently not included in the VM. 
* I didn't test the VM against all build-targets.

## Future & Maintenance

I don't plan to maintain the project beyond the summer term 2017 of RWTH Aachen University (30/09/2017). This is because i only need this project for a pracitcal project seminar. However, feel free to fork this repository and maintain your own fork.
