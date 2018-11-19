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

