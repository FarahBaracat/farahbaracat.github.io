---
layout: post
title: Day 90 in Farina's Lab - Creating a Flask API
tags: [ICL Project]
include_toc: true
---

To inferace between MATLAB and python scripts, I am implementing an API encapsulating all the Python code for 
training SNN and making inference.

### Developping API using Flask
- To create the API itself, it is a straightforward task. There are many tutorials online (Medium [articles](https://towardsdatascience.com/creating-restful-apis-using-flask-and-python-655bad51b24))
- To test the API, I could do that from the terminal using `curl`. In my case since I was using local host I could 
  just run:

     `curl -v http://127.0.0.1:5000/infer`
- I was a bit confused about the difference between the having a URL with a trailing slash vs without one. As 
  explained in the Medium article, accessing a URL that is defined with `\` always redirects to this URL even if you 
  forgot to add the `\` in the call. For URLs defined without the trailing slask, if you try to access it with an 
  added `\` would give a `404`
- There are several ways to pass data to the web App:
  - It also possible to pass data in the query strings. This 
    doesn't 
    require the 
    user to take action 
    though. More 
    details are in this [article.](https://www.digitalocean.
    com/community/tutorials/processing-incoming-request-data-in-flask)
  - Another way is through form data. In this case the incoming data comes from a form (well surprise 😀) that is 
    sent with the POST request. The data is then passed to the App without directly showing in the URL.


---
### Testing with MATLAB functions: webread/webwrite
- I first run the development server. "Flask provides a run command to run the application with a development 
  server" (from [documentation](https://flask.palletsprojects.com/en/2.2.x/server/)) which would be running on my local 
  host.
- Then used `data = webread('http://127.0.0.1:5000/infer')` to get the mock predictions 🥳. It returns a struct with 
  fields `predictions` (as specified in the `jsonify` response).
- I then modified the code to add the POST method and managed to send data with the request to the Web App. It worked 💃🏻
- Next, since up until now my API is running on a developemnt server, I started looking into how to serve it on a 
  production server: WSGI (Web Server Gateway Interface) came about.


---
### Deployment: Web Server Gateway Interface (WSGI)
A very informative [Medium article.](https://medium.com/analytics-vidhya/what-is-wsgi-web-server-gateway-interface-ed2d290449e)
- the API (Application Programming Inferface) I am creating with Flask is a web application.
- This web application needs to be running somewhere on a server which would then receive and handle the incoming 
  requests from various users. Makes sense?

![web_server_api](/blog/figures/web_server_web_app.png)

- Now how these two components should interact? The standards for carrying out the communication is the WSGI.
![web_server_WSGI](/blog/figures/web_server_WSGI.png)
- This mediator block is a WSGI container. There are many containers available today such as Gunicorn, CherryPi, 
  uWSGI. These containers take up the requests from the web server and can invoke Python application through 
  'callable' objects.
- Some of the most common WSGI servers used for deploying Flask applications are Gunicorn
