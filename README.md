# Chef Solo Knife example

Example provisioning a server using Chef Solo and Knife. Configuration is a LEMP stack with users and basic security settings.

Based on this excellent guide: [http://leopard.in.ua/2013/01/04/chef-solo-getting-started-part-1/](http://leopard.in.ua/2013/01/04/chef-solo-getting-started-part-1/)

This repo also includes a simple [Vagrant](http://www.vagrantup.com/) VM for quick testing of your configuration/cookbooks.

## Usage

1. Install gem dependencies:

	````
	$ gem install bundler && bundle install
	````
2. Edit `Cheffile` to add/remove cookbooks.

3. Install cookbooks:

	````
	$ librarian-chef install
	````

4. Rename `nodes/10.10.10.10.json` to match your host ip and edit configuration with real passwords etc.

5. Rename `data_bags/users/example-user.json` to match your user and edit the user configuration.

6. Prepare machine using Knife:

	````
	$ knife solo prepare user@host
	````

7. Cook machine:

	````
	$ knife solo cook user@host
	````

8. Your machine should now be provisioned and you should be able to SSH in with your user!

## Custom cookbook

This repo includes a custom cookbook for setting hostname and configuring basic firewall rules ([UFW](https://help.ubuntu.com/community/UFW)). Please see `site-cookbooks/custom`.

## Test configuration in Vagrant

1. Spin up a test VM with Vagrant:

	````
	$ vagrant up
	````

2. The VM will get the hostname 10.10.10.10, make sure your configuration can be found in `nodes/10.10.10.10.json` and run:

	````
	$ knife solo prepare root@10.10.10.10
	````

	Note: You might have to change the root password to something you know before starting via `vagrant ssh`.

3. Cook Vagrant VM:

	````
	$ knife solo cook root@10.10.10.10
	````


