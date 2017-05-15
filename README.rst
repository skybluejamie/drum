Wikipeace
====
Wikipeace is a Wiki for all solutions, built using Drum https://github.com/stephenmcd/drum, which on turn is built using `Mezzanine`_.

Check out the blog post `Building Social Apps with Mezzanine`_,
which contains a detailed walk-through of how Drum was built. A
`live demo of Drum`_ is also available.

Dependencies
============

Wikipeace is a forked version of Drum and requires Mezzanine to also be installed. This repository is designed for contributors to update certain features for the site Wikipeace.

Installation
============

Create a virtualenv, download this repository and run in terminal::
    
    $ source activate "virtualenv_name"
    $ git clone https://github.com/skybluejamie/wikipeace.git
    $ cd wikipeace
    $ python setup.py develop

Once installed, the command ``mezzanine-project`` can be used to
create a new Mezzanine project, with Drum installed, in similar
fashion to ``django-admin.py``. The wikipeace site can then be tested and modified on your local machine::

    # FIXME: add new instructions of how to create a project with wikipeace
    $ mezzanine-project -a drum project_name
    $ cd project_name
    $ python manage.py createdb --noinput
    $ python manage.py runserver
    
The site will then run locally and you can test and make changes to do it in the wikipeace repository. 
Here we specify the ``-a`` switch for the ``mezzanine-project`` command,
which tells it to use an alternative package (drum) for the project
template to use. Both Mezzanine and Drum contain a project template
package containing the ``settings.py`` and ``urls.py`` modules for an
initial project.

.. note::

    The ``createdb`` is a shortcut for using Django's ``syncdb``
    command and setting the initial migration state. You
    can alternatively use ``syncdb`` and ``migrate`` if preferred.

You should then be able to browse to http://127.0.0.1:8000/admin/ and
log in using the default account (``username: admin, password:
default``). If you'd like to specify a different username and password
during set up, simply exclude the ``--noinput`` option included above
when running ``createdb``.

Auto Tagging
============

Drum provides some basic support for automatically tagging new links
as they're added. This is first configured by setting the ``AUTO_TAG``
setting to ``True``. With that set, when a new link is added, its
given title is broken up into keywords, and if those keywords already
exist as tags in the database, they're applied to the newly added link.

This means that for auto-tagging to work, the tags must already exist
in the database. You can either add them manually via the admin (under
the "Keywords" section), or if you have a large number of existing
links, you can use the ``auto_tag`` management command Drum provides,
which will analyse the titles of all your existing links, and provide
tags it extracts from them. This makes use of the `topia.termextract`_
package which you'll first need to install::

    python manage.py auto_tag --generate=100 --assign --remove

The ``--generate`` option must be provided to extract tags, and limits
the number of tags extracted. Generally more tags will be extracted
than are relevant, depending on your existing set of links, so
experiment with different values here. You'll likely want to review all
the tags added, deleting some and manually editing others, via the
Django admin interface. The ``--assign`` option will go back and assign
all tags in the database to all links in the database, as would occur
if they were newly created. The ``--remove`` option will cause all
existing tags to be removed.

You can also define your own tag extraction function, if splitting the
title on spaces doesn't suffice. To do so, define the setting
``AUTO_TAG_FUNCTION`` which should contain a string with the Python
dotted path to your custom tag function. The function will be given an
unsaved ``Link`` object, and should return a sequence of tags to add.


Contributing
============
Information to come soon

Support
=======

