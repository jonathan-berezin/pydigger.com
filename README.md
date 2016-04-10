Source code of http://pydigger.com/


TODO
======

* Switch to the GitHub API
* Search should also look into keywords
* How many times each keyword is used?
* Find and list dependencies
* Report when the URL provided as GitHub repo is invalid. (e.g. returns 404)
  Maybe even compare some files?

* Is there a requirements.txt file? and test_requirements.txt ?
   package==version
   package>=version


* Why are there maintainers where the value is "" and others where it is null ?
* Sats: author_email (look for null, "", "UNKNOWN", in the e_mail look for strings that don't look e-mail. e.g. no @)
* locate "keywords" fields that are not space separated lists (e.g. pyspotify-connect)



* Code to update items
* Have a data for "updated" when we last updated the entry

* Show statistics about each field we show
* List the packages that don't have a VCS listed, find out if they have VCS listed elsewhere, or if they are using some other VCS
* Create a list of "known licenses" and the names people use to refer to each license, link to the real license.
* Show licenses that don't fit in any of the "known licenses"
* On the package specific page link to explanations on how to correct where a field is missing.
* Show Green and red bars for each package on the listing page
* Find out what other services are used by Python packages
* Check for common files in Python packages
* Show which packages have strange version numbers (that cannot be parsed by ) https://www.python.org/dev/peps/pep-0396/
* Is the cheesecake_code_kwalitee_id still relevant?

* Statistics about types of "home_page" fields
* "home_page": "http://pmbio.github.io/limix/",
* "home_page": "http://ianmiell.github.io/shutit/",



Description
==============
Fetching RSS feed of recently uploaded packages https://pypi.python.org/pypi?%3Aaction=rss

Each entry in the RSS feed looks like this

  <item>
    <title>package-name 0.2.1</title>
    <link>http://pypi.python.org/pypi/package-name/0.2.1</link>
    <description>short description</description>
    <pubDate>25 Mar 2016 12:36:38 GMT</pubDate>
  </item>

Accessing the link followed by /json returns a JSON structure with a lot more details about
the specific version of the given package. Like this:

{
    "info": {
        "maintainer": null,
        "docs_url": null,
        "requires_python": null,
        "maintainer_email": null,
        "cheesecake_code_kwalitee_id": null,
        "keywords": null,
        "package_url": "http://pypi.python.org/pypi/PACKAGE",
        "author": "Person Name",
        "author_email": "user@domain",
        "download_url": "UNKNOWN",
        "platform": "UNKNOWN",
        "version": "1.0.0",
        "cheesecake_documentation_id": null,
        "_pypi_hidden": false,
        "description": "Some long description....",
        "release_url": "http://pypi.python.org/pypi/PACKAGE/1.0.0",
        "downloads": {
            "last_month": 0,
            "last_week": 0,
            "last_day": 0
        },
        "_pypi_ordering": 0,
        "classifiers": [
            "Development Status :: 5 - Production/Stable",
            "Intended Audience :: Science/Research",
            "License :: OSI Approved :: GNU General Public License (GPL)",
            "Operating System :: OS Independent",
            "Programming Language :: Python",
            "Programming Language :: Python :: 2",
            "Programming Language :: Python :: 3"
        ],
        "name": "PACKAGE",
        "bugtrack_url": null,
        "license": "GPLv3",
        "summary": "short summary",
        "home_page": "URL",
        "cheesecake_installability_id": null
    },
    "releases": {
        "1.0.0": []
    },
    "urls": []
}


We save these two data structures and in addition we try to determine if the package has Git repository and
if Travis-CI is configured in that repository.

We cannot store the data received from Pypi as it is in a MongoDB database as
it has places where the version number is a key and has . in it which cannot be
a key in MongoDB.
