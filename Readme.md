# About
> Documentation about server Rancher with docker server.
> Installation with simple server docker 
> Run Certification with cert-manager - cluster production
> Creation cluster with provider digitalocean
> Make volumes, services
> Run pipelines fichiers with digitalocean
> How to resolve node stopped

# How to run this in local environment
### - Check your ruby --version 2.X
### - Build up in terminal: gem install bundler
### - Creation make file: Gemfile # incluide the next lines 
> source 'https://rubygems.org'
> gem 'github-pages', group: :jekyll_plugins
### - Building in directory: bundle install
### - Run server local: bundle exec jekyll serve --source=docs --incremental