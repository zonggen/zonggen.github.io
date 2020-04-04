# zonggen.github.io

## Installation
 ### Ubuntu :
 Install dependencies:
 - `$ sudo apt-get install ruby-full build-essential zlib1g-dev`

 Avoid installing as `root` user:
 - `$ echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc`
 - `$ echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc`
 - `$ echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc`
 - `$ source ~/.bashrc`

 Install `jekyll` and `bundler`:
 - `$ gem install jekyll`
 - `$ gem install bundler -v 12.3.3`

 Run:
 - `$ jekyll serve`
 - `Browse to http://localhost:4000`

 ### Fedora :
 Install dependencies:
 - `$ sudo dnf install ruby ruby-devel @development-tools`
 - `$ gem install jekyll`
 - `$ gem install bundler -v 12.3.3`
 - `$ bundle install`

 Run:
 - `$ jekyll serve`
 - `Browse to http://localhost:4000`

## Related links:
- https://jekyllrb.com/docs/installation/ubuntu/
- https://developer.fedoraproject.org/start/sw/web-app/jekyll.html
- Original template: https://github.com/janczizikow/sleek
