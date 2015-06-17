# GP-Electron

Electron wrapper for GraphPaper using [Electrometeor](https://github.com/sircharleswatson/Electrometeor).

## Build step

Clone this repo

    git clone https://github.com/yathit/gp-electron.git
    
Add GraphPaper web app
    
    cd gp-electron
    rm -rf meteor
    git clone https://github.com/xumx/graphpaper meteor
    
Follow [Electrometeor](https://github.com/sircharleswatson/Electrometeor) for detail, briefly
    
    npm install
    ./script/setup.js
    ./script/run.js
    ./script/dist.js

## Electron settings

In run.js

    process.env.DDP_DEFAULT_CONNECTION_URL = 'http://graphpaper.co';

In index.js

    userEnv.DDP_DEFAULT_CONNECTION_URL = 'http://graphpaper.co';

Copy setting file to resource

    cp settings.js dist/osx/Electrometeor.app/Contents/Resources/app/resources/


## Workaround

Issue https://github.com/sircharleswatson/Electrometeor/issues/11

      setTimeout(function () {
        var fullURL = rootURL + ':' + webPort;
        callback(fullURL, nodeChild, mongoChild);
      }, 2000);

Sometimes `meteor build` does not product dist package. Amend dist.js file as follow

    exec(meteorCommand + ' build --directory ../. --architecture os.osx.x86_64 --server graphpaper.co:80');
    
If mongo stuck due to lock, delete lock file
    
    rm ~/Library/Application\ Support/Electrometeor/data/mongod.lock

Module loading in String.js file. Remove module loading parts.



## Problems

1. Facebook Oauth dance
2. Bootstrap css reset
3. module loading in App client. Electron browser define `module`, but it is not load like AMD module. So js file rely on `module` to load fail.

## Todo

1. We don't use mongodb backend in the app, but still it still require and running.
2. App naming and app info

