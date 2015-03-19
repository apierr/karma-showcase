[![Build Status](https://travis-ci.org/antonio-pierro/karma-showcase.svg?branch=master)](https://travis-ci.org/antonio-pierro/karma-showcase)

## Karma showcase

### Prerequisites
 
 1. Node.js
 
        > node -v # it should be at least 0.10
        > npm -v # it should be at least 0.5

 2. Configure git
    - Create a repository on github and name it “karma-showcase”
    - Open your shell and run the following commands:

            > mkdir karma-showcase; cd karma-showcase
            > git init
            > git remote add origin git@github.com:<github-account>/karma-showcase.git

### Install karma

1. Create a package.json

        > npm init # create the package.json file
        > git add package.json
        > git commit -m ”Generated package.json”
        
2. Install locally the karma packages needed for the test

        > npm install karma --save
        > npm install karma-jasmine --save
        > npm install karma-chrome-launcher --save
        > npm install karma-firefox-launcher --save

3. Create a `.gitignore` file to avoid polluting your repository with vendors 

        > echo "node_modules" > .gitignore
        >export PATH=$PATH:node_modules/karma/bin

### Create your first simple test

  - Create the following test file:
    
         /* test/first.spec.js */
        describe('True test', function() {
            it('Should be true', function() {
                expect(true).toBeTruthy();
            });
        });
        
        > git add test
        > git commit -m”Created my first test with karma-jasmine”

  - Create the karma configuration file

        > karma init
  
        # Respond to the question in the following ways:
    
        Which testing framework do you want to use ? jasmine
        Do you want to use Require.js ?no
        Do you want to capture any browsers automatically ? <choose Chrome or Firefox>
        What is the location of your source and test files ? test/*spec.js
        Do you want Karma to watch all the files and run the tests on change ? yes
    
        > git add karma.conf.js
        > git commit -m”Generated the karma.conf.js”

### Run your first test

      > karma start karma.conf.js

### Use Travis CI

  1. Find your repository on https://travis-ci.org/ and set to on the build.
  2. create the file .travis.yml

          # .travis.yml
          language: node_js
          node_js:
            - "0.12"

  3. Create and copy the “Build Status” mardown in your README.md file

          > git add README.md
          > git commit -m”Added ”

  4. The test on travis should fail. try to fix the error.

### Solutions:

  1. in your test you need to specify the path to karma   
      
        node_modules/karma/bin/karma

  2. Travis cannot start chrome browser, so you should change it in PhantomJS and you need also to install karma-phantomjs-launcher
