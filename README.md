# DemoWebServer
To create your own web server using python

Install cherrypy using pip on windows
```
pip install cherrypy
```

Then write the below python code to display hello world in your webserver and configured port.
save it in a file name let say my_fisrt_web_server.py

```
import cherrypy

config = {
    'global' : {
        'server.socket_host' : '127.0.0.1',
        'server.socket_port' : 5081
        # 'server.socket_port' : 8080
    }
}

class demoExample:
   def index(self):
       return "Hello, Sakti!!!"

   index.exposed = True

cherrypy.quickstart(demoExample(), '/', config)
```

then runn the python script my_fisrt_web_server.py. Once you run, you will get the url http://127.0.0.1:5081 like this.
copy paset the url in the browser. You will see hellow world displayed in the page.

# Example to returm radom values in the webpage

save then below code in a file say myRandom.py

```
import random
import string
import cherrypy

config = {
    'global' : {
        'server.socket_host' : '127.0.0.1',
        'server.socket_port' : 5082
        # 'server.socket_port' : 8080
    }
}

class StringMaker(object):
   @cherrypy.expose
   def index(self):
      return "Hello! How are you?"

   @cherrypy.expose
   def generate(self, length=9):
      return ''.join(random.sample(string.hexdigits, int(length)))

if __name__ == '__main__':
   cherrypy.quickstart(StringMaker(), '/', config)
```
Then run the script and check the url http://localhost:5082/generate?length=32 or http://localhost:5082/generate for the expected result.

# Example using static html page

Create Below directory structure
```
.
├── app.py
└── docs
    ├── a.html
    ├── b.html
    └── index.html
```
app.py
```
#!/usr/bin/env python3


import os

import cherrypy


path   = os.path.abspath(os.path.dirname(__file__))
config = {
  'global' : {
    'server.socket_host' : '127.0.0.1',
    'server.socket_port' : 5085,
    'server.thread_pool' : 8,
  },
  '/docs' : {
    'tools.staticdir.on'    : True,
    'tools.staticdir.dir'   : os.path.join(path, 'docs'),
    'tools.staticdir.index' : 'index.html',
    'tools.gzip.on'         : True
  }
}


class App:

  @cherrypy.expose
  def index(self):
    return '''Some dynamic content<br/><a href="/docs">See docs</a>'''


if __name__ == '__main__':
  cherrypy.quickstart(App(), '/', config)

```

docs/index.html
```
 <!DOCTYPE html>
<html>
<head>
  <title>Docs index</title>
</head>
<body>
  <p><a href='/'>Back to home page</a> (not relevant from file://)</p>
  <p><a href='a.html'>See A</a></p>
  <p><a href='b.html'>See B</a></p>
</body>
</html>
```

docs/a.html
```
<!DOCTYPE html>
<html>
<head>
  <title>A page</title>
</head>
<body>
  <p><a href='index.html'>Back to index</a></p>
  <p><a href='b.html'>See B</a></p>
</body>
</html>
```

docs/b.html
```
<!DOCTYPE html>
<html>
<head>
  <title>B page</title>
</head>
<body>
  <p><a href='index.html'>Back to index</a></p>
  <p><a href='a.html'>See A</a></p>
</body>
</html>
```
