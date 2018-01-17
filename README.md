# SELinux Game

This site is the source which provides http://selinuxgame.org/ and is compiled
by [Jekyll](https://jekyllrb.com/). The site itself is hosted with
[Github Pages](https://pages.github.com/).


## Authors

The theme is originally forked from the [Lanyon theme] provided by
[Mark Otto](https://github.com/mdo).

For the SELinux Game content see the [Authors page](AUTHORS.md).


## Building Locally with Vagrant and Fedora

1. `vagrant init fedora/27-cloud-base && vagrant up`
2. ssh to the box and tunnel port 4000 with: `vagrant ssh -- -L 4000:127.0.0.1:4000`
3. Install necessary deps with dnf `sudo dnf install ruby ruby-devel gcc redhat-rpm-config git zlib-devel`
4. Clone the repo into this box: `git clone https://github.com/SELinuxGame/selinuxgame.org.git`
5. Go into the repo directory: `cd selinuxgame.org`
6. Install Bundler for ruby: `gem install bundler`
7. Install the ruby dependencies with `bundle install`
8. Build and serve Jekyll: `bundle exec jekyll serve`
9. Browse on your host at: http://127.0.0.1:4000/


## License

Open sourced under the [MIT license](LICENSE.md).
