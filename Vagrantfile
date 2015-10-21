Vagrant::Config.run do |config|
  config.vm.box = "ubuntu-14.04"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.network :hostonly, "10.10.10.10"

  config.vm.share_folder("site", "/home/vagrant/site", ".", :nfs => false)
  config.vm.provision :shell, :path => "./_conf/vagrant_setup.sh"
end
