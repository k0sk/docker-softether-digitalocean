BASIC_ARGS = "-d --net host --name softether"
CONFIG_ARGS = "-v /vagrant/vpnserver/vpn_server.config:/usr/local/vpnserver/vpn_server.config"

Vagrant.configure("2") do |config|
  config.vm.provider :digital_ocean do |provider, override|
    override.ssh.private_key_path = ENV["DO_KEY_PATH"]
    override.vm.box = "digital_ocean"
    override.vm.box_url = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    provider.token = ENV["DO_PERSONAL_ACCESS_TOKEN"]
    provider.image = "ubuntu-14-10-x64"
    provider.region = "nyc2"
    provider.size = "512mb"

    override.vm.provision "docker" do |d|
      d.pull_images "frosquin/softether"

      if File.exist?("./vpnserver/vpn_server.config")
        ARGS = BASIC_ARGS + CONFIG_ARGS
      else
        ARGS = BASIC_ARGS
      end

      d.run "frosquin/softether",
        args: ARGS
    end
  end
end
