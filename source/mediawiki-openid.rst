OpenId plugin for MediaWiki
===========================

Prerequisites:

#. MediaWiki installed already
#. These following packages already installed on the system which 
   is hosting MediaWiki: ``gmp``, ``mcrypt``,  ``curl``, ``openssl``, ``xml``. 
   Generally all but ``gmp`` and ``mcrypt`` is not installed on a standard 
   Ubuntu system. For that just do a ``sudo apt-get install php5-mcrypt 
   php5-gmp``.


Assumption: ``$IP`` is assumed to be the root of the wiki directory.




* Get the source code for the extension into ``$IP/extensions`` directory ::

	cd extensions
	git clone http://gerrit.wikimedia.org/r/p/mediawiki/extensions/OpenID.git 

* Check your mediawiki version by going to ``<your_wiki_URL>/index.php?title=Special:Version``. Say your version is 1.19.x. 
  Check out branch for the same version of OpenID code::

	git branch -a 
	git checkout -b stable_REL1_19 origin/REL1_19 
 
* Add this line at the end of LocalSettings.php file::

	require_once "$IP/extensions/OpenID/OpenID.php"; 
 
* Now install Auth subdirectory as following::

	cd $IP/extensions/OpenID 
	git clone http://github.com/openid/php-openid.git 
	mv php-openid/Auth Auth 
	rm -r php-openid 
	cd $IP 
	php maintenance/update.php --conf LocalSettings.php 
 
* Restart apache server::

	/etc/init.d/apache2 restart 
 
* Editing 'Login required' page.  
  Add these lines to LocalSettings.php and restart mediawiki and apache server::

	$wgGroupPermissions['user']['editprotected'] = true; 
	$wgGroupPermissions['user']['editinterface'] = true; 
 
Now you can edit the ``<your_wiki_URL>/jiocloud/index.phpmediawiki:loginreqpagetext`` page, which is a protected page, which is presented when the user is not logged in.
