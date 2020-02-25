============================================================
Create a new GitHub Pages site for all your docs with Sphinx
============================================================

Create GitHub repo
===================

Log in to github create new repo and initiallize with a readme.

If you haven't already install Sphinx on the computer you will be working on
instructions can be found here -  (link to docs)

Open a terminal
::

    $ git clone "your repo url here"
    $ cd 'repo name'
    $ mkdir docs
    $ cd docs 

Now we will use Sphinx to set the repo up for us::

    $ sphinx_quickstart

As we move through the config the main options paid attention to were
::

    > Separate source and build directories (y/n) [n]: y 
    > githubpages: create .nojekyll file to publish the document on GitHub pages (y/n) [n]: y 


Conf.py Changes
==================

in conf.py change the following
::

    html_static_path = ['_static'] to html_static_path = []

    html_theme = 'alabaster' to html_theme = 'sphinx_rtd_theme'

in extensions add
::

    'sphinx.ext.githubpages',
    'recommonmark',

This is also the page you will define HTML theme options on. The ones for this page are;
::

    html_theme_options = {
        'canonical_url': '',
        #'analytics_id': 'UA-XXXXXXX-1',  #  Provided by Google in your dashboard
        'logo_only': False,
        'display_version': True,
        'prev_next_buttons_location': 'bottom',
        'style_external_links': False,
        #'vcs_pageview_mode': '',
        'style_nav_header_background': 'green',
        # Toc options
        'collapse_navigation': True,
        'sticky_navigation': True,
        'navigation_depth': 4,
        'includehidden': True,
        'titles_only': False
    }


GitHub Setup
==================
Click on profile photo on Github to go to your account. Go to:

    > Account Settings -> Developer Settings -> Personal access tokens

| Generate a new token and give it the name ``GH_TOKEN`` and check Repo to give it full push/pull permission.
| *Copy it somewhere safe. You cannot reaccess it*

Go back to your project repo where your docs are.

Create a new branch called ``gh-pages``

Go to the repo settings and scroll down to GitHub Pages section and select the gh_pages branch as source
    
    - This option is only available from repo/project based Github pages. If building a user page it has to be built from Master


Travis-CI Setup
==================
Go to https://www.travis-ci.org and sign in using your GitHub ID

Click + to view your Repos

Sync your account if you do not see your Repo

In the root of your repo create a travis.yml file
  This includes the information Travis will use to build your site

  My file looks like this:
  ------------------------

  language: python

  install:
  - pip install sphinx sphinx_rtd_theme mock recommonmark


  script:
  - sphinx-build -Wv docs/source docs/build/html

  deploy:
  # publish docs on push
  - provider: pages
    skip_cleanup: true
    keep-history: false
    github_token: $GH_TOKEN  #this is the token added to env variables in travis the name is case sensitive
    local_dir: docs/build/html
    on:
      branch:  master

  ----------------------------------------------------------------

  More info on this can be found here 
     - https://docs.travis-ci.com/user/deployment/pages/



  in terminal go your docs directory and add your files and commit your initoal Changes

  git add --all
  git commit -a -m 'adding initial changes to repo and trigger first build'
