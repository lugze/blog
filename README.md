# blog

Link to the live blog.

* https://lugze.github.io/blog/

# Howto build locally

Clone the repo.

````
git clone git@github.com:lugze/blog.git
cd blog
````

Check if Ruby is installed locally

````
ruby -v
````

Get the latest bundler

````
gem install bundler
bundle update --bundler
````
Install the dependencies
````
bundle install
````

Run the server locally

````
bundle exec jekyll serve
````

Browse to http://localhost:4000
