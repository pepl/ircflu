ircflu
======

ircflu is an IRC bot written in Go with a flexible message- & command-handler.
Among its advanced features are a catserver which allows you to forward incoming
messages from a TCP socket straight to an IRC channel and an integrated HTTP
server, ready to process incoming JSON-API calls.

At Tomahawk (http://tomahawk-player.org) we're all pretty much addicted to IRC.
We use it not only to coordinate our development efforts and communicate, but
also to get alerted about source code changes on GitHub, when a ticket gets
updated or a service on our servers runs into an issue. We can even use it to
trigger commands being executed on our servers, e.g. to deploy the latest
source code.

ircflu can do all that for us... except the communicating. It's not that kind
of chatbot.

## Installation

Make sure you have a working Go environment. See the [install instructions](http://golang.org/doc/install.html).

To install / compile ircflu from source, simply run:

    go get github.com/fluffle/goirc/client
    go get github.com/hoisie/web
    git clone git://github.com/muesli/ircflu.git
    cd ircflu
    go build

To run the application you will need to specify a few options:

    ./ircflu -ircnick="somenickname" -irchost="some.server:6667" -ircchannel="#yourircchannel" -authpassword "yourpassword"

Run ircflu -help to see a full list of options!

## Make it do stuff

When started with its default options, ircflu will listen for incoming
connections on TCP port 12345. You can now send messages to an IRC channel
from your favorite shell script or any terminal:

    echo "This will be sent to IRC." | netcat -q0 127.0.0.1 12345

ircflu also runs an integrated HTTP server on port 12346, processing incoming
GitHub (on /github) & GitLab (on /gitlab) web-hook calls which are triggered
by a commit to your git repository. ircflu will in turn notify you on IRC.

It comes with a simplistic authentication system (!auth), supports aliases for
commands (!alias) and executing external applications (!exec), forwarding their
output to IRC.

More soon!

Continous integration: [![Build Status](https://secure.travis-ci.org/muesli/ircflu.png)](http://travis-ci.org/muesli/ircflu)
