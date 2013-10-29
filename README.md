Analytics
=========
BSkyB wrapper for Adobe Sitecat analytics JS.

## Using Analytics
Please read through 'Getting Started' here http://skyglobal.github.io/analytics

## Building Analytics Locally

### Code structure
- grunt/js/
  The source code, unminified and ready to work on.  

- grunt/js/analytics.js
  The public API is created here (returned at the bottom). This file brings together files from /core, /plugins and /utils.

- grunt/js/wiki.js
  JS to make the demo page work.  This JS is also used as part of the unit testing.

- grunt/sass/
  The look and feel for the wiki pages.  

- dist/
  Compiled (via grunt) code

- _includes/
  Source documentation for using the API.

- _site/
  Compiled (via jekyll) documentation for using the API.

- app.rb
  A basic Sinatra server for running the functional tests

- test/
  the functional + unit tests for the API

- circle.yml
  Configuration for the CI server

- config.ru
  Configuration for running the Sinatra server

- Gruntfile.js
  Configuration for grunt tasks - to do with compiling the javascript

### Prerequisites

- RVM
- Ruby (version 1.9.3 or later)
- npm

### Setup
1. Clone the repository from Github onto your local machine
2. Install npm
  - echo 'export PATH=/usr/local/bin:$PATH' >> ~/.bashrc
  - . ~/.bashrc
  - mkdir /usr/local
  - mkdir ~/node-latest-install
  - cd ~/node-latest-install
  - curl http://nodejs.org/dist/node-latest.tar.gz | tar xz --strip-components=1
  - ./configure --prefix=/usr/local
  - make install # ok, fine, this step probably takes more than 30 seconds...
  - curl https://npmjs.org/install.sh | sh
3. Install grunt either globally, or run the following to use the bundled project grunt
  - npm install

### Running

1. In the root of the project, run the following:
  - bundle
  - jekyll serve --watch
2. In another terminal run 'grunt watch' (add ' --beautify' to help debugging)
3. You should be able to see the documentation site in your browser on http://localhost:4000

### Testing
Tests are in the test directory and use minitest and capybara for functional and mocha for unit. 
These tests are automatically run on the CircleCI server upon pushing to Github

To run the functional test suite, simply type `rake functional` in your terminal.
To run the unit test suite, type `grunt test` in your terminal.


### Deployment
In order to release a new version of the library, the version number in _config.yml must be
incremented following the rules below: 

#### Versioning
This library should follow the [Semantic versioning
specification](http://semver.org/). In short, that means the following:

Version: X.Y.Z

- API changes that are **not backwards compatible**, and break existing
  calls using the API must increment the X value.

- API changes that introduce **new backwards compatible changes**, or **change the
  internals**, but not the interface, of existing methods will increment the
  Y value.

- **Patches or bug fixes** that are backwards compatible should increment the
  Z value.


Upon commiting and pushing your code to Github, the CI server will run through
the functional tests and - if there are no errors - a new version of the library
will be deployed to the CDN using the version number specified in the
_config.yml file.
