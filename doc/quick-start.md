<style>
body { width:650px }
iframe { width:650px; height: 550px; }
</style>

<a href="https://github.com/dcposch/scramble"><img style="position: absolute; top: 0; right: 0; border: 0;" src="https://s3.amazonaws.com/github/ribbons/forkme_right_gray_6d6d6d.png" alt="Fork me on GitHub"></a>


SCRAMBLE.io Quick Start
======

Run a Scramble server, the easy way
----
On a freshly installed Ubuntu server:

    wget -O - https://scramble.io/bin/quick-start.sh | /bin/bash

Boom. This interactively installs MySQL and configures Scramble.

Follow the instructions, then go to `http://localhost:8888` to see results.


Run a Scramble server, the slightly less easy way
----
If you want to do it manually, the quick-start script doubles as an install guide:

<iframe src="/bin/quick-start.sh" style="border:none"></iframe>

Go produces statically linked binaries with no dependencies. It's awesome.

You can run the database server and application server on different machines. 
Just edit `~/.scramble/db.config` on the app server.

I'll add a mechanism to sign the `scramble` binary soon. More on that bleow.


Run a real Scrable server
----
Next, you'll need to serve a domain with HTTPS, not `http://localhost:8888/`.

### Hosting
Linode and AWS both work well. 
I recommend Linode, since they have a free real-time monitoring tool.

Install Scramble as described above.

I recommend [locking down your server][TODO] to avoid being compromised.

### Domain name
I've had a good experience with Gandi, which also provides DNS and SSL certificates.

### SSL Certificate
You'll have to buy an SSL certificate for your domain. Install it on your server:

TODO

### Nginx
Configure Nginx. Here's the configuration for `scramble.io`. Fill in your own details.

TODO

### Cron
Back up the database. Rotate the logs. Both should be copied to a different disk, ideally in a different location. Again, here's the configuration for `scramble.io`:

TODO

If you've made it this far, you have a usable secure mail server. Thanks for helping people communicate privately, defending their rights.


Sign Scramble releases
----
As mentioned above, I need a mechanism to sign Scramble releases.

That way, people who run Scramble servers will be protected even if this website is compromised or someone compels me to serve a bad version of Scramble, as long as they check the signature.

I would like each release to be signed not just by myself, but by a group of volunteers in different countries.

I propose the following process:

* We develop, test and code review in public.
* We announce a new release candidate, specifying the git commit hash.
* You, the volunteer, check out the specified commit. 
  Git verifies hashes, so you have confidence that all volunteers are looking at the same code.
* You compile the binary.
  Scramble will have a repeatable build process, so each volunteer produces an identical binary from source.
* You sign the binary.
* We publish the new release, displaying all the signatures on this page.
* People who run Scramble servers are invited to upgrade, checking the signatures.


Develop Scramble
----

Prerequisites: Git, Go, and Screen

To install this on Ubuntu:

    sudo apt-get install git golang screen

Then, set up Go. For example:

    cd ~
    mkdir -p go/src
    echo "export GOPATH=/home/dc/go" >> ~/.bashrc
    echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.bashrc
    source ~/.bashrc

Then, run Scramble:

    cd ~/go/src
    git clone git@github.com:dcposch/scramble
    cd scramble
    make

Navigate to `http://localhost:8888`.

### Coding style

* Go
  * Standard formatting. Using `gofmt` before committing. 
  * Write godoc. 
  * Write tests.
* Javascript
  * No semicolons at the end of the line.
  * Always use braces. 
  * Write comments before each function. 
  * We'll add jslint or something soon.
* Both languages
  * No lines over 80 characters. Unix line endings. Tabs, not spaces. 
  * Use consisent prefixes and suffixes in variable names to avoid confusion. 
    For example, `plainSubject`, `cipherSubject`, `plainBody`, `cipherBody`.

And to steal from the Zen of Python...

* Explicit is better than implicit
* Flat is better than nested
* Beautiful is better than ugly

### First pull request
You can make your first pull request in an hour or so!

* Fix a bug: https://github.com/dcposch/scramble/issues
* Write a unit test
* Pull requests that only add comments or documentation are still cool

