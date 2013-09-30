Jenkins
=======

Jenkins runs on a 4GB VM in the Rackspace cloud. Less than 4GB will cause some tests to OOM, so 4GB is the minimum.

Jenkins is installed like so:::

    wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
    sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
    sudo apt-get update
    sudo apt-get install jenkins

Once installed, add the following plugins:

* GitHub API Plugin
* GitHub Authentication Plugin (Sometimes referred to as Github OAuth Plugin)
* GitHub plugin
* Git plugin
* Job Configuration History Plugin

#. Follow the `Github authentication plugin's setup instructions`_ on how to register an app on Github and retrieve the Client ID and Client Secret.
#. Go to `Jenkins's Configure Global Security`_ page.
#. Enable security
#. Choose GitHub Authentication as the Security Realm. Leave the URI's as the defaults.
#. For now, leave Authorisation as "Anyone can do anything".
#. Check "Prevent cross site request forgery exploits".
#. Save
#. Login to create your account.
#. Go to Jenkins's Configure Global Security page.
#. Check "Github Commiter Authorization Strategy" under Authorization.
#. Add your own name under "Admin User Names".
#. Put "JioCloud" in "Participant in Organization". (Be mindful of capitalization)
#. Check "Grant READ permissions for /github-webhook"
#. Save
#. Log out
#. Log in, this time as the jiojenkins user.
#. Go to `user configuration page`_ to fetch API token.
#. Create /etc/jenkens_jobs/jenkins_jobs.ini with the following contents::

    [jenkins]
    user=jiojenkins
    password=the API token
    url=http://localhost:8080/

#. Check out https://github.com/JioCloud/jenkins-jobs (anywhere, e.g. in your home dir)
#. Run ``./apply.sh``.


.. _Github authentication plugin's setup instructions: https://wiki.jenkins-ci.org/display/JENKINS/Github+OAuth+Plugin
.. _Jenkins's Configure Global Security: http://jiocloud.rustedhalo.com:8080/configureSecurity/?
.. _user configuration page: http://jiocloud.rustedhalo.com:8080/user/jiojenkins/configure
