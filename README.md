# bag-describe

A simple shell script that generates file format description data for all
files in a BagIt bag.


## Overview

This script calls upon an instance of the 
[DAITSS Format Description Service](https://github.com/daitss/describe)
to generate PREMIS records characterizing each file in a BagIt data directory.
The resulting records are saved in a new tag directory named "premis" inside
the bag's root.

This code is fairly trivial, and can be easily adapted to other use cases.


## Setting up a local instance of the Format Description Service

The best way to use this script is to have a local instance of the Format 
Description Service running on your machine, though technically it doesn't
matter what machine you run it on since all of the communication happens over
HTTP.

These steps should help you to set up and run such an instance with minimal
effort.

Requirements:

*   Linux or Mac OSX
*   [RVM](https://rvm.io/)
*   [Java](https://www.java.com/)

(Before you begin: Make sure a Java JRE or JDK is installed somewhere and that
the `JAVA_HOME` environment variable is set to the path where it is located.)

1.  Open a Linux/Mac command line and `cd` into the directory where you want 
    the description service to reside. (Inside of this directory is fine if
    you're not sure.)
2.  `curl -L https://github.com/daitss/describe/archive/5035ef1a9a4dd0aea1eedc3f4ad5e8a619974b95.tar.gz | tar zx`
3.  `cd describe-5035ef1a9a4dd0aea1eedc3f4ad5e8a619974b95`
4.  `rvm use 1.9.3`
5.  `bundle install` (you may run into issues here depending on your platform; 
    refer to the README.md file in the `describe-5035...` directory for more 
    information on setting up the Format Description Service if needed)
6.  `export DAITSS_CONFIG=daitss-config.example.yml`
7.  `export VIRTUAL_HOSTNAME=describe.example.org`
8.  `bundle exec thin start`


## Using the bag-describe script

If needed, edit the `bag-describe` file in this directory using a text editor
and change the location specified on the line that reads

    DESCRIBE_URL=http://localhost:3000

to the actual URL and port of your Description Service instance.

Then simply run

    ./describe-bag path/to/your/bag

to start the process. The resulting PREMIS records will be created in a new
directory inside your bag's root called `premis`.


## License

See LICENSE.txt
