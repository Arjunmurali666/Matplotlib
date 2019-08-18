# Matplotlib
## Python - This is a python code written to print the IP and the number of connections From the access log as a barchart. 

I have used the module matplotlib to plot the barchart. matplotlib is a python 2D plotting library which produces publication quality figures in a variety of hardcopy formats and interactive environments across platforms. 

You can generate plots, histograms, power Spectra, bar charts, error charts, scatterplots..etc with just a few lines of code. 

In this code, It will take the most common 4 IPs and in the bar chart it will show the number of connections in Y axis and the source IP in X axis. 


```python
import os
import logparser
import collections
import requests
from matplotlib import style
from matplotlib import pyplot as plt
style.use('ggplot')

def info(*,ip=None,key=None):

  if ip != None and key != None:
    url = 'http://api.ipstack.com/{}?access_key={}'.format(ip,key)
    response = requests.get(url)
    geodata = response.json()
    code = geodata['country_code']
    return (code)


logFile = 'access.log'    
        
ipCounter = collections.Counter()

        
with open(logFile,'r') as fh:
    
    for logLine in fh:
      
        ip = logparser.parser(logLine)['host'] 
        
        ipCounter.update([ip])
        
for ip,hit in ipCounter.most_common(4):
    x2 = ip.split()
    y2 = hit
    try:
        code = info(ip=ip,key='604a43d7a0a1971161d9a6da7194a3c2').split()
    except:
        code = 'system'
    print('{:20} : {} {}'.format(ip,hit,code))
    plt.bar(x2, hit, align='center', alpha=1)
    plt.ylabel('connections')
    plt.xlabel('IP')
    plt.title('Counting number of connections from the IPs')
```

## The output of the code will look like as following.

!(https://ibb.co/znyLgr1)
<a href="https://ibb.co/znyLgr1"><img src="https://i.ibb.co/K0MQgXY/barchart-2.jpg" alt="barchart-2" border="0"></a><br /><a target='_blank' href='https://movieplotholes.com/the-hobbit-an-unexpected-journey'>the hobbit an unexpected journey movie</a><br />
