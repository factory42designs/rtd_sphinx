==================================
Setting up Sphinx on Ubuntu
==================================

for refenece I used this page to get started: https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html


First we must install and setup pip

    ``$ sudo apt-get install python-pip`` 

Then install Sphinx

    ``$ pip install sphinx``

When I installed sphinx I had an error that ~/.local was not in PATH. This is easily remedied by editing ~/.bashrc

    ``$ nano ~/.bashrc``

    paste at the end:
    
    ``export PATH=$PATH:~/.local/bin``

    and source the PATH by running: 

    ``$ source ~/.bashrc``

Now you should be able to run shinx-quickstart with no issues on the next steps

