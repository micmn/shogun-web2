Shogun-Web2
===========
Re-write and re-design of the Shogun website

currently running at: [http://shogun-web.herokuapp.com/](http://shogun-web.herokuapp.com/)


Overview
--------
Shogun-Web2 is written in python using [Flask](http://flask.pocoo.org/). The application has no database and instead pulls most of its data from other locations via APIs.

[Twitter Bootstrap](http://getbootstrap.com/) is used for the frontend framework along with the [Stanley Theme](http://www.blacktie.co/2014/01/stanley-freelancer-theme/)


Details
-------
* Latest News section pulls from our Twitter feed using the Twitter API

* Recent Activity shows the most recent commits from Github using their API

* The main showcase reel at the top and the multi carousel of notebooks at the bottom fetches notebooks and demos from directories on the production server. Several notebooks are included in this repo and the site will use them when running it locally.

* The site features a link to the latest Shogun docs generated by doxygen

* IRC logs are recorded by an irssi bot on our channel running on the same server as the website. A cron job runs every 17 minutes copying the latest irc logs into HTML (using [logs2html](https://pypi.python.org/pypi/irclog2html) for the site

* The blog is a combination of several RSS feeds of interest and is fetched using the [Google Feeds Javascript API](https://developers.google.com/feed/). The combination feed itself is generated by another Flask application running on Heroku [http://shogun-planet.herokuapp.com/feed](http://shogun-planet.herokuapp.com/feed)


Deploying
---------
The site is currently deployed to [Heroku](https://www.heroku.com/) under Kevin Hughes' account (kevinhughes27 on Github) until we move it to the Shogun-toolbox.org server.

To deploy run script/deploy.sh

If you need to update credentials on Heroku run `script/creds2heroku.sh`

Developing
----------
To run the app locally you can either run `./script/server.sh` or use the Heroku toolbelt manual and run `foreman start`. Both of these approaches will export the required environment variables before starting the main program. In order to run the app locally with full functionality you will need a copy of the credentials in the `.env` file. Message someone to get these credentials securely.

### Embedding markdown files

To embed a markdown file from the `docs submodule` (see [shogun-toolbox/docs](https://github.com/shogun-toolbox/docs)).

_Prerequisites:_

  * `DOCS_SUBMODULE_DIR` const in `shogun_web.py` defines the relative path to app's root folder
  * Fetch the docs submodule into the `docs` folder in the root


Create a `<div>` in the template file (e.g. `templates/install.html`) based on the following template:

```
    <div class="md" data-type="md" data-url="/docs/README.md">
      <div class="md-container" style="text-align: justify"></div>
    </div>
```

This example also shows how to pass a paragraph style (here: text-align).


For more detail see `static/javascripts/markdown.js`.
