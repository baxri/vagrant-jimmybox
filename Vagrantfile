# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    # FIX vagrant share
    ###########################################################################
    # In some cases, we recognized that vagrant share breaks after some clicks
    # We enabled --natdnshostresolver1 to fix this
    #
    # If you have troubles with this setting, please just disable the next 3 lines

    config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end

    # BOX SETTINGS
    config.vm.box = "sternpunkt/jimmybox"

    # NETWORKING
    ############################################################################

    config.vm.hostname = "web"

    # Private Network
    config.vm.network "private_network", ip: "192.168.10.10"

    # port forwarding must be enabled for vagrant share
    config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true

    # Public network:
    # uncomment the lines and add your own config (bridge, ip, etc.)

    # config.vm.network "public_network",
    # :bridge => "en0: WLAN (Airport)",
    # ip: "192.168.10.201", :netmask => "255.255.255.0", auto_config: true

    # SYNCED FOLDERS
    ############################################################################

    # DEFAULT:
    config.vm.synced_folder ".", "/var/www", :mount_options => ["dmode=777", "fmode=666"]

    # NFS:
    # you should try NFS share - it performs much better than the default synced folder!
    # config.vm.synced_folder "./", "/var/www", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

    # RSYNC:
    # if you are using a framework that contains many files rsync can provide best performance
    # You can use vagrant rsync-auto to sync changes automatically to your vagrant box.
    # config.vm.synced_folder "./", "/var/www", type: "rsync", rsync__auto: true
	
	
	config.vm.provision "shell", inline: <<-SHELL
   
		sudo cp /var/www/sites/vhosts /etc/apache2/sites-available/vhosts.conf		
		sudo a2ensite vhosts		
		
		sudo service apache2 restart		
	
    SHELL
	
	config.vm.box_download_insecure = true
end
