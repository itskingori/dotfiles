setup:
	# install homebrew
	/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
	
	# configure homebrew with bundle feature, see:
	# https://robots.thoughtbot.com/brewfile-a-gemfile-but-for-homebrew
	brew tap homebrew/bundle

install:
	# install packages specified in 'Brewfile', see:
	# https://robots.thoughtbot.com/brewfile-a-gemfile-but-for-homebrew
	brew bundle

	# verify the success of the rbenv installation and
	# detect common issues
	curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash	

	# install ruby 2.3.3 via rbenv
	rbenv install 2.3.3 --skip-existing
	rbenv local 2.3.3
	gem install bundler

	# install ruby 2.4.2 via rbenv
	rbenv install 2.4.2 --skip-existing
	rbenv local 2.4.2
	gem install bundler

	# set ruby 2.4.2 to global version
	rbenv global 2.4.2


