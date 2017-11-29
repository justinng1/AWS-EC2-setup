# This document shows how to setup Jupyter notebook on my EC2 instance.

Instructions were pulled from here: https://medium.com/@GalarnykMichael/aws-ec2-part-4-starting-a-jupyter-ipython-notebook-server-on-aws-549d87a55ba9

1. find sha1 hash of your password for Jupyter Notebook.

a) run ipython in the terminal.
b) type the following code:
from IPython.lib import passwd
passwd()
c) copy down the sha1 string.

2. configure Jupyter Notebook.

a) run the following in the terminal.

jupyter notebook --generate-config 
mkdir certs
cd certs
sudo openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem
cd ~/.jupyter/
vi jupyter_notebook_config.py

b) paste these lines into jupyter_notebook.config.py.
```python
c = get_config()
c.IPKernelApp.pylab = 'inline' 
c.NotebookApp.certfile = u'/home/ec2-user/certs/mycert.pem' 
c.NotebookApp.ip = '*' 
c.NotebookApp.open_browser = False 

# Your password below will be whatever you copied earlier 
c.NotebookApp.password = u'sha1:941c93244463:0a28b4a9a472da0dc28e79351660964ab81605ae' 
c.NotebookApp.port = 8888
```

3. run jupyter notebook.
jupyter notebook

4. To access your server, enter https://ip-address:port/
