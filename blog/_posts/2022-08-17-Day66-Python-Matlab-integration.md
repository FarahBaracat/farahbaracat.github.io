---
layout: post
title: Day 66 - How to deploy a trained SNN in MATLAB?
tags: [ICL Project]
include_toc: true
---

I am looking to integrate the scripts I have in Python for training and inference with Deren's scripts for 
decomposition, recording,...etc.

The main question I am researching is:

 > Is it better to look for ways to call Python functions from within MATLAB or look for ways to deploy the trained 
  model (e.g deplotung the model as a RESTful API)?


# Ways to serve ML model
- This is referred to as model deployment. Given a trained model, how can we make it usable/ accessible to end users.

## Model deployment as a web service
- We put the model inside a web service. An easy way to create a web service 
  in Python is using **Flask**: 
 > is a web application framework written in Python. It is a Python-based micro 
  framework 
  used 
  for developing small-scale websites.  It allow us to easily create a RESTful APIs in Python and hence can 
  help end 
  users interact with the trained model (Python code) directly from their web browser without needing any libraries, 
  code files, etc. 
 
- With Flask we can turn a function into a web service and invoke it. We set up a Flask server that requests 
  predictions from model.py and returns the predictions.
- We setup a Flask app and run it now (make it up and ready to get requests). With that we would have created a 
  web application


- There are mainly two ways or stages to deploying the web server/app: either using localhost (that is local 
    server), or sharing it 
    over the public internet so that other people can access it.
    - [_Localhost_](https://blog.hubspot.com/website/what-is-localhost): in a computer network, localhost "is a hostname that refers to the computer that is executing a 
      program". The IP address starting with '127' defines loopback address. It references a device on your private, 
      local network. When accessing the localhost of any computer, we make requests to the IP address '127.0.0.1"

 
---
### Interlude on API and RESTful
- **Application Protocol Interface (API)** is a set of definitions and protocols for building and integrating 
  application software. It is the mediator between a user/client and the resources or web services.
- **REST** stands for representation state transfer is a set of architectural constraints. It is not a protocol or a 
  standard

---

### Step-by-step process to deploy the model as API
<figure>
<img src="/blog/figures/deploy_model_flask.png" alt="drawing" width="2500"/>
</figure>

- Once we create a web service, we can then POST requests to the localhost to get the predictions as JSON.
- In MATLAB, I can then use [_webread_](https://uk.mathworks.com/help/matlab/ref/webread.html#buqbzbb) function in MATLAB to POST requests.
