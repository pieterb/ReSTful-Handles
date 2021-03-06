Installation
============

Requirements
------------

### JRuby
First of all, this software requires JRuby, as it interfaces with the Java client library of the Handle System.
JRuby can be installed in many ways.
You can go to the [JRuby web site](http://jruby.org/) and download it from there.
The developers of this software prefer using the [Ruby Version Manager (RVM)](http://beginrescueend.com/) for managing multiple Ruby installations on a single machine, and for managing multiple gemsets.

After installing JRuby, make sure that the interpreter runs in _1.9_ _mode_.
This is done by adding option `--1.9` to environment variable `JRUBY_OPTS`.
If you use `RVM`, you might consider using an `.rvmrc` document.
There's an example of such a document in the distribution, by executing

    rvm rvmrc

inside the root of this distribution.

### Handle System v7
You'll need a running Handle System installation.
Details can be found at the [Handle System web site](http://www.handle.net/).

The web service needs to know the location of your Handle System installation.
Create a symbolic link inside the Web Service top level directory called `hsj`, pointing to `$HS_DISTRO_ROOT/lib`.

### Sequel
Sequel is a Ruby database abstraction layer and Object-Relational Mapper (ORM).
For performance reasons, we don't use the ORM features.

Installing `sequel` is easy:

    gem install sequel

Depending on the kind of database you're using underneath the Handle System,
you'll probably need to install some database handler as well.
The service developers use gem `jdbc-mysql` in order to connect to their
MySQL databases.

### Rackful
[Rackful](http://pieterb.github.com/Rackful/) is a library to build ReSTful web
services on top of [Rack](http://rack.rubyforge.org/doc/).

You might want to read the
[Rack interface specification](http://rack.rubyforge.org/doc/SPEC.html)
and [other Rack documentation]() as well.

    gem install rackful

Configuration
-------------

The web service comes preconfigured for HTTP Digest authentication.
You'll need to create two configuration files for this to work, though:

### General configuration
The default installation expects some configuration information in file `config.rb`.
You'll find a sample configuration file called `config.rb.example` in the distribution.
Copy or rename this file to `config.rb` and edit it to your situation:

    cp -a config.rb.example config.rb
    $EDITOR config.rb

### User accounts
In the default configuration, account information is expected in file `secrets/users.rb`.
From the installation root, do the following:

    cd secrets/
    cp -a users.rb.example users.rb
    $EDITOR users.rb

Running!
--------

At this point, you should be able to start the web service:

    rackup

By default, this will start a Webrick web server, listening to port 9292.

If you'd like to use another web server, another port number, another authentication method,
then check out the Rack documentation,
and start editing the rackup configuration file `config.ru`.
That files contains a lot of in-line documentation that hopefully gets you started.
