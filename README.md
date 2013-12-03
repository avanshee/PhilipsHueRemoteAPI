#Philips Hue Remote Control API

Sicne the Philips Hue [Portal API](http://developers.meethue.com/5_portalapi.html) is not yet released, this API is developed so that it is possible to control philips hue remotely.

The work is based on [Hacking Lightbulbs: Security Evaluation of the Philips Hue Personal Wireless Lighting System](http://www.dhanjani.com/docs/Hacking%20Lighbulbs%20Hue%20Dhanjani%202013.pdf) by [Nitesh Dhanjani](http://www.dhanjani.com/about.html)

The API server is running on top of [flask](http://flask.pocoo.org/) python web framework.

##How Does This Remote API Work?
I wrote a overview explanation of the remote API hack of the Philips Hue in a blog post here: [http://paulshi.github.io/technical/2013/11/27/Philips-Hue-Remote-API-Explained.html](http://paulshi.github.io/technical/2013/11/27/Philips-Hue-Remote-API-Explained.html)

##RESTful API Endpoint

####/api
Transparent API

 * PUT/POST works just like official API
 * The response from PUT/POST is always 200. The call to the API endpoint discovered by the paper only give limited response
 * GET will get all the current status of the Philips Hue bridge

Example:

```
Official API Endpoint : /api/<username>/lights/<id>/state
Official API Method: PUT
Official API Data: {"ct":153, "colormode":"ct"}

Custom API Endpoint : http://localhost:5000/api/lights/<id>/state
Custom API Method: PUT
Custom API Data: EXACT THE SAME AS ABOVE
```

It should in theory support all official PUT/POST API calls to the URL endpoint of `/api/username/*******`

So any official `/api/username/**********` with method PUT/POST
can be achieved using `http://localhost:5000/api/***********` with method PUT/POST

The response is always 200 unfortunately unless the request body is not JSON format, in which case it gaves an error message

##Setup
Fill in `credentials.py.sample` and rename it to ```credentials.py```
In order for it to work you need a `token` and `bridgeID` as explained in my blog [post](http://paulshi.github.io/technical/2013/11/27/Philips-Hue-Remote-API-Explained.html) mentioned earlier.

##Install
Setup virtual environment

```
virtualenv ev
source ev/bin/activate
```

Install required packages

```
pip install -r requirements.txt
```

##Run

```
python hueapiserver.py
```

##Limitations
With```/api``` you can do PUT/POST to control correctly, GET will get you all the status. Other method is not supported at the moment


##Documentation
http://philips-hue-remote-api.readthedocs.org/

##License

```
The MIT License (MIT)

Copyright (c) 2013 Jarvis Inc (by Jianer Shi hipaulshi@gmail.com)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```

[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/jarvisinc/philipshueremoteapi/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

