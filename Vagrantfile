# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box      = 'ubuntu/bionic64' # 18.04
  config.vm.hostname = 'rails-dev-box'
  
  # Forward ports
  [
    3000, # Rails Puma
    5432, # Postgres
    1080, # Mailcatcher web ui
    4040  # Ngrok web ui
  ].each do |p|
    config.vm.network :forwarded_port, guest: p, host: p
  end

  config.ssh.forward_agent = true
  
  config.vm.provision :shell, path: 'bootstrap.sh', keep_color: true

  config.vm.synced_folder ".", "/vagrant"

  config.vm.provider 'virtualbox' do |v|
    v.memory = ENV.fetch('RAILS_DEV_BOX_RAM', 2048).to_i
    v.cpus   = ENV.fetch('RAILS_DEV_BOX_CPUS', 2).to_i
  end

end
