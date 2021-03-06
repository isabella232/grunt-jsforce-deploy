# grunt-jsforce-deploy
[![Build Status](https://travis-ci.org/jsforce/grunt-jsforce-deploy.svg?branch=master)](https://travis-ci.org/jsforce/grunt-jsforce-deploy)

A grunt task for deploying Salesforce package, using JSforce's Metadata API feature.
As it is implemented purely in Node.js, you do not have to setup Force.com Migration Tool (Ant, Java) anymore.

## Setup

```
$ npm init
$ npm install grunt grunt-jsforce-deploy --save-dev
```

## Example 

### Project Directory

```
├── Gruntfile.js
├── package.json
└── pkg
    ├── classes
    ├── objects
    ├── package.xml
    ├── pages
    └── staticresources
```

### Gruntfile.js

```javascript
module.exports = function(grunt) {
  grunt.loadNpmTasks("grunt-jsforce-deploy");

  grunt.initConfig({
    jsforce_deploy: {
      pkg: {
        expand: true,
        cwd: ".",
        src: [ "pkg/**" ]
      },
      options: {
        username: process.env.SF_USERNAME,
        password: process.env.SF_PASSWORD,
//        loginUrl: "https://test.salesforce.com",
//        pollTimeout: 120*1000,  // set polling timeout to 120sec (default is 60sec)
//        pollInterval: 10*1000,  // set polling interval to 10sec (default is 5sec)
      }
    }
  });

  grunt.registerTask("deploy", [ "jsforce_deploy" ]);
};
```

### Deploy

```
$ SF_USERNAME=username@example.com SF_PASSWORD=yourpassword grunt deploy
```

or if you have `foreman` installed, create `.env` file with above credential information, and execute :

```
$ foreman run grunt deploy
```
