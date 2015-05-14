Vagrant.configure("2") do |config|
  config.vm.provider :digital_ocean do |provider, override|
    override.ssh.private_key_path = "~/.ssh/id_rsa"
    override.vm.box = "digital_ocean"
    override.vm.box_url = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    provider.token = `envchain do printenv PERSONAL_ACCESS_TOKEN`.chomp
    provider.image = "ubuntu-14-10-x64"
    provider.region = "nyc2"
    provider.size = "512mb"

    override.vm.provision "docker" do |d|
      d.pull_images "frosquin/softether"
      d.run "frosquin/softether",
        args: "-d --net host --name softether"
    end
  end
end
