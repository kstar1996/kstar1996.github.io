---
layout: post
title:  "Introduction to Flask"
author: Eujin
categories: [ flask ]
image: 
tags: []
---

## Introduction to Flask

As I mentioned in the previous post, I will not be explaining about installing Flask. There are lots of articles online that explain how to install it. Please go and search the internet.

Now, if you have Flask installed, let's get started. Whenever we learn something new, we start off with the simple "Hello World." Here is a minimal Flask application.

```python
// An highlighted block
# import Flask class
# an instance of this class is the app
from flask import Flask 

# creating instance of the class
app = Flask(__name__)

# using the route() decorator to tell Flask what URL should trigger the function 
@app.route('/')

# the function is given a name which is also used to generate URLs for that particular function
# returns the message we want to display
def hello_world():
    return 'Hello, World!'
```
