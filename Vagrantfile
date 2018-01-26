---
layout: blank
---
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  scenarios = [{% for scenario in site.scenarios %}'{{ scenario.slug }}', {% endfor %} 'tutorial']

  scenarios.each do |scenario|
      config.vm.synced_folder ".", "/vagrant", disabled: true
      # Create the "selinuxgame" box
      config.vm.define scenario do |selinuxgame|
        selinuxgame.vm.box = "selinuxgame/" + scenario
        selinuxgame.vm.host_name = "selinuxgame.example.com"

        selinuxgame.vm.provider :libvirt do |domain, override|
            domain.cpus = 1
            # In some cases, the guest gets stuck at "Waiting for domain to get an IP address..." if
            # the default cpu_mode, 'host-model', is used. Using 'host-passthrough' cpu_mode prevents
            # VM migration between hosts with different CPUs. However, selinuxgame environments are
            # expected to live on a single host for the duration of their existence. Due to this known
            # issue and our use case, the default cpu_mode is overridden.
            domain.cpu_mode = "host-passthrough"
            domain.graphics_type = "spice"
            domain.memory = 1024
            domain.video_type = "qxl"

        end
     end
  end
end
