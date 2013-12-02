#Chef Blueprint: openvpn_server

##Description

A Chef Blueprint for an OpenVPN server.

##Requirements

* Chef 0.10.10 or higher (earlier versions may work with some cookbooks/recipes)
* A Linux host or guest environment
* Vagrant 1.2 or higher (if using Vagrant)
* vagrant-omnibus plugin (if using Vagrant)
* Git (if checking out the source from GitHub)

##Usage

See the Quick Start below to get started.

###Cookbooks

The core cookbook used is Opscode's openvpn (https://github.com/opscode-cookbooks/openvpn).
By default `Cheffile.full` is used. See `share/librarian/Cheffile.*` for other cookbook setups that can be used with this blueprint. 

##Quick Start

###VirtualBox with Vagrant

####Install VirtualBox

Follow the VirtualBox (or your OS/distribution) documentation to install VirtualBox if not already installed, see https://www.virtualbox.org/wiki/Documentation

####Install Vagrant

Follow the Vagrant (or your OS/distribution) documentation to install Vagrant (latest version recommended), see http://docs.vagrantup.com/v2/installation/index.html

####Install Librarian for Chef

	$ gem install librarian-chef --no-rdoc --no-ri

####Clone the openvpn_server Blueprint

	$	git clone https://github.com/chef-blueprints/openvpn_server_.git

####Setup a Cheffile

By default `Cheffile` is a symlink to `share/librarian/Cheffile.full` which includes other cookbooks used with the server.
`Cheffile.lock` will display the details of their upstream sources.

To setup a minimal server with only the openvpm cookbook:

	$ ln -fsv ./share/librarian/Cheffile.minimal ./Cheffile

####Install the cookbooks

This will fetch the cookbooks as specified in the Cheffile:

	$ librarian-chef install --clean
  
####Setup node.json

For the 'minimal' cookbook setup:

	$ cp -v share/chef/node.minimal.json node.json

For the 'full' cookbook setup:

	$ cp -v share/chef/node.full.json node.json
  
####Setup a Vagrantfile

Copy the default Vagrantfile from `share/vagrant`:

	$ cp -v share/vagrant/Vagrantfile.default Vagrantfile

####Run with Vagrant

Already up'd a openvpn_server?

	#vagrant status                   # check vm status
	#vagrant reload                   # reload the vm
	#vagrant provision                # (re-)provision the vm
	#vagrant suspend                  # suspend the vm
	#vagrant halt                     # power down the vm
	#vagrant destroy                  # destroy the vm
	#vagrant box remove linux_box     # remove the box

#####Run the virtual machine

Add a new box and up it (default in `Vagrantfile` is Debian 7.10, Ubuntu 12.04 is also tested and supported).

Vagrant will automatically add a new box per the Vagrantfile if not already created (including download).

	$ vagrant up

Need debug?

	$ VAGRANT_LOG=debug vagrant up
	
This uses the `Vagrantfile` and `node.json` (for the Chef Solo provisioning) residing in the root of the repository, copied above.

##Chef Solo

Using the Vagrant/VirtualBox process above is recommended for desktop/workstations users and will provide an operational Linux box, out-of-box.
The instructions below demonstrate usage with Chef Solo standalone. Commands are relative the root of the repository.

	# chef-solo -c share/chef/solo.rb
	
By default this uses the `node.json`. You can easily switch the JSON attributes used with another example:

	# chef-solo -c share/chef/solo.rb -j /etc/chef/node.json
	
Its also possible to run with the cookbooks source as remote. This is handy because no Git checkout is needed:

	# chef-solo -r https://github.com/chef-blueprints/openvpn_server/tarball/master
	
And with a specific tag such as `Rev1`:

	# chef-solo -r https://github.com/chef-blueprints/openvpn_server/tarball/rev1

For more information on using Chef Solo, see http://wiki.opscode.com/display/chef/Chef+Solo

##RightScale

Search the MultiCloud marketplace for the 'OpenVPN ServerTemplate' (http://rightscale.com/library).

#Using Librarian

##Install Librarian

	# gem install librarian --no-rdoc --no-ri

##Updating cookbooks

Set this environment variable to strip .git from each cookbook checkout:

	$ export LIBRARIAN_CHEF_INSTALL__STRIP_DOT_GIT=1

To update a cookbook (example, openvpn):
	
	$ librarian-chef update openvpn

To refresh all the cookbooks in `cookbooks/` per the `Cheffile`, run the following:

	$ librarian-chef install
	
#Errata

TODO: MANIFEST file.

##License and Author

Author:: Chris Fordham (<chris [at] fordham [hyphon] nagy [dot] id [dot] au>)

Copyright 2013, Chris Fordham

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and