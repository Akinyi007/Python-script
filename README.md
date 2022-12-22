# Python-script


import requests
from flask import Flask, request
from collections import defaultdict

app = Flask(name)

# create a dict to store IP-request count mapping
ip_count = defaultdict(int)

# define the maximum number of requests allowed from a single IP
MAX_REQUESTS_PER_IP = 10

@app.route('/', methods=['GET'])
def hello():
   # get the IP address of the requesting client
   ip = request.remote_addr
   # increment the request count for the IP
   ip_count[ip] += 1
   # if the request count is greater than MAX_REQUESTS_PER_IP, return error
   if ip_count[ip] > MAX_REQUESTS_PER_IP:
       return 'Too many requests from this IP', 429
   # otherwise return a successful response
   return 'Hello World!', 200

if name == 'main':
   app.run()
