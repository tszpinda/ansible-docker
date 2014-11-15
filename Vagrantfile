# -*- mode: ruby -*-
# vi: set ft=ruby : 
# David Lutz's Multi VM Vagrantfile
# inspired from Mark Barger's https://gist.github.com/2404910
 
boxes = [
  { :name => :an1,    :role => 'docker_dr',  :ip => '192.168.33.10', :ssh_port => 2201, :http_fwd => 9990,  :cpus =>1, :shares => true },
  { :name => :an2,    :role => 'docker',     :ip => '192.168.33.11', :ssh_port => 2202, :mysql_fwd => 9901, :cpus =>1, :shares => true },
  { :name => :an3,    :role => 'docker',     :ip => '192.168.33.12', :ssh_port => 2203, :http_fwd => 9992,  :cpus =>1, :shares => true },
  { :name => :an4,    :role => 'docker',     :ip => '192.168.33.13', :ssh_port => 2204, :http_fwd => 9993,  :cpus =>1, :shares => true},
]
 
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
 
  boxes.each do |opts|
 
    config.vm.define opts[:name] do |config|
 #    config.vm.box        = "ubuntu-11.10-server-amd64-ruby1.9.3"
 #    config.vm.box_url    = "http://hostname/boxes/ubuntu-11.10-server-amd64-ruby1.9.3.box"
     config.vm.box = "https://oss-binaries.phusionpassenger.com/vagrant/boxes/latest/ubuntu-14.04-amd64-vbox.box"
 #    config.vm.customize  ["modifyvm", :id, "--memory", 1024]
     #todo make this an option
 
 #    config.vm.forward_port  80, opts[:http_fwd] if opts[:http_fwd]
 #    config.vm.forward_port  3306, opts[:mysql_fwd] if opts[:mysql_fwd]
#      config.vm.network       :hostonly, opts[:ip]
      config.vm.network "private_network", ip: opts[:ip]
      config.vm.host_name =   "%s.vagrant" % opts[:name].to_s
 
      # config.vm.share_folder  "stuff", "/usr/local/stuff", "~/Projects/stuff", :nfs => true if opts[:shares]
      # use nfs rather than VirtualBox shared files.  It's heaps faster.
 
      #config.vm.forward_port  22, opts[:ssh_port], :auto => true
 
      # cpus defaults to 1
	   config.vm.provider "virtualbox" do |v|
  	 	  v.memory = 512
  		  v.cpus = 1
  	 	  v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
      end
    end
  end
end
