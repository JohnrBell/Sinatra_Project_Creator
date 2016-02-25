# Sinatra_Project_Creator

Just put this in your bash profile. Call it by saying ```sinatra_touch [project name]```

```
function sinatra_touch(){
  if [ "$#" -ne 1 ]
  then
    echo "You must provide a project name. Usage: 'sinatra_touch [name]'"
    return
  fi
    mkdir $1
    cd $1
    mkdir views
      echo -e '"Hello World."' > views/index.erb
      echo -e '<!doctype html>\n<html>\n<head>\n  <link href="/css/style.css" rel="stylesheet" type="text/css">\n</head>\n<body>\n  <div class="container">\n    <%= yield %>\n  </div>\n</body>\n</html>\n<script src="/js/jquery.js" type="text/javascript"></script>\n<script src="/js/script.js" type="text/javascript"></script>' > views/layout.erb
    mkdir public
      mkdir public/img
      mkdir public/css
        touch public/css/style.css
      mkdir public/js 
      
        #gets jQuery, checks for successful download. 
        curl -f http://code.jquery.com/jquery-2.2.1.min.js > public/js/jquery.js
        if [ -s public/js/jquery.js ]
        then
          echo 'jQuery Download Successful.'
        else
          rm public/js/jquery.js
          echo 'ERROR: jQuery download failed, file removed.'
        fi

        echo -e '"use strict";\n(function(){\n\n})();' > public/js/script.js
    mkdir lib
    printf 'module Sinatra\n  class Server < Sinatra::Base\n    get "/" do\n      erb :index\n    end\n  end\nend' > server.rb
    printf 'require "sinatra/base"\nrequire "sinatra/reloader"\nrequire_relative "server"\nrun Sinatra::Server' > config.ru
    subl . #change this line to your editor of choice. 
}
```
