OpenShift - MediaWiki
=====================

This repository is designed to be used with http://openshift.redhat.com/
applications.  To use, just follow the quickstart below.


Quickstart
----------

1. Create an account at http://openshift.redhat.com/
2. Create a php-5.3 application and attach mysql to it:

        rhc app create -a mediawiki -t php-5.3
        rhc app cartridge add -a mediawiki -c mysql-5.1

3. Add this upstream mediawiki repo

        cd mediawiki
        git remote add upstream -m master git://github.com/openshift/mediawiki-example.git
        git pull -s recursive -X theirs upstream master

4. Then push the repo upstream

        git push

5. That's it, you can now checkout your application at:

    http://mediawiki-$yourlogin.rhcloud.com

    Default Admin Username: `Admin`
    Default Password: `OpenShiftAdmin`


Updates
-------

In order to update or upgrade to the latest mediawiki, you'll need to re-pull
and re-push.

1. Pull from upstream:

        cd mediawiki/
        git pull -s recursive -X theirs upstream master

2. Push the new changes upstream

        git push

3. Update MediaWiki to the new version by visiting
    http://mediawiki-$yourlogin.rhcloud.com/mw-config/
    or by running `php update.php` in the maintenance directory on your server.


Repo layout
-----------

`php/` - Externally exposed php code goes here

`libs/` - Additional libraries

`misc/` - For not-externally exposed php code

`../data` - For persistent data

`deplist.txt` - list of pears to install

`.openshift/action_hooks/build` - Script that gets run every push, just prior to
    starting your app


Notes about layout
------------------

Please leave php, libs and data directories but feel free to create additional
directories if needed.

_**Note**: Every time you push, everything in your remote repo dir gets recreated
please store long term items (like an sqlite database) in `../data` which will
persist between pushes of your repo._


deplist.txt
-----------

A list of pears to install, line by line on the server.  This will happen when
the user git pushes.


Additional information
----------------------

Link to additional information will be here, when we have it :)
