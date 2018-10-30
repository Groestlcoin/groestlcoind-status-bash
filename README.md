# groestlcoin-status-bash
This is small bash script to generate a Groestlcoin node status page.
It uses simple templating to separate data retrieval and logic from HTML generation.

#### Table oc Contents

1. [Requirements](#requirements)
2. [Getting Started](#getting-started)
3. [Configuration](#configuration)
4. [Licensing](#licensing)

## Requirements

To run this script, you will need:

* A Groestlcoin node.
* The groestlcoin client _groestlcoin-cli_ with access to the groestlcoin node.
* A web-server to deliver the generated html file.*

## Getting Started

On a standard groestlcoin core node, _groestlcoin-cli_ is installed at /usr/local/bin and has access to the groestlcoind when you run it as the user you installed the groestlcoind configuration.
So all you need is _bash_ and _sed_ and any web server set up to deliver your status page.

Copy the files in the _app_ directory to your groestlcoin node, i.e. in the home directory of your groestlcoin user.
Create a directory that serves as the docroot of your status page and set this directory as the _outputdir_ in the configuration part of _refreshe_status_page_.
Make sure that _refresh_status_page_ is executable (chmod +x generate_status_page).

Run the script every 10 minutes by adding to your crontab:

    */10 * *   *   *     /path/to/your/refresh_status_page

## Configuration

At the beginning of the script, you can set several variables:

* outputdir - the directory where the files are generated/copied
* IP - the IP address of your groestlcoin node

And of cause you can adjust the HTML template _status_template_.
In the template you can use all the variables that you have set in the configuration section and all the values that are returned by _groestlcoin-cli getblockchaininfo_.
Usefull parameters are:

* version
* protocolversion
* blocks
* connections
* difficulty

These are set as shell variables so insert them as ${variable}.

## Important

As the templates is evaluated by the shell, properly escape all double quotes.

## Licensing

* Copyright (c) 2015 [Martin Meier](http://www.edv-beratung-meier.de)
* Distributed under the terms of the [MIT License](LICENSE)
