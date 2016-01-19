# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 4000, host: 4000, auto_correct: true

  config.vm.provision "shell", inline: <<-SHELL
    # configure proxy (if required)
    # export https_proxy=yourproxy:port
    # export http_proxy=yourproxy:port

    sudo -E apt-add-repository -y ppa:brightbox/ruby-ng
    sudo -E apt-get update
    sudo -E apt-get install -y software-properties-common ruby2.2-dev ruby2.2 nodejs git zlib1g-dev
    sudo -E gem install jekyll github-pages

    # I use --force_polling because on windows, changes are not detected otherwise.
    # To start jekyll, run: (it could be a startup script)
    # jekyll serve --force_polling --drafts --host 0.0.0.0 --source /vagrant
  SHELL
end
