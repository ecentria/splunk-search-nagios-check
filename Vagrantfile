$script = <<SCRIPT
rpm -ivh http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
yum install -y python-pip mc
pip install splunk-sdk argparse
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "puppetlabs/centos-6.6-64-puppet"
  config.vm.provision "shell", inline: $script
end
