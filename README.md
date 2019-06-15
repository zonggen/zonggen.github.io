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
 - `$ gem install bundler -v 1.12`
 
 Run:
 - `$ jekyll serve`
 
 ### Fedora :
 Install dependencies:
 - `$ sudo dnf install ruby-devel`
 - `$ gem install jekyll`
 - `$ gem install bundler -v 1.12`
 
 Run:
 - `$ jekyll serve`
 
### Related links:
 - https://jekyllrb.com/docs/installation/ubuntu/
 - https://developer.fedoraproject.org/start/sw/web-app/jekyll.html
 - Original template: https://github.com/janczizikow/sleek
