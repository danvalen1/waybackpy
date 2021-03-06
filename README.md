# waybackpy

![contributions welcome](https://img.shields.io/static/v1.svg?label=Contributions&message=Welcome&color=0059b3&style=flat-square)
[![Build Status](https://img.shields.io/travis/akamhy/waybackpy.svg?label=Travis%20CI&logo=travis&style=flat-square)](https://travis-ci.org/akamhy/waybackpy)
[![codecov](https://codecov.io/gh/akamhy/waybackpy/branch/master/graph/badge.svg)](https://codecov.io/gh/akamhy/waybackpy)
[![Downloads](https://pepy.tech/badge/waybackpy/month)](https://pepy.tech/project/waybackpy/month)
[![Release](https://img.shields.io/github/v/release/akamhy/waybackpy.svg)](https://github.com/akamhy/waybackpy/releases)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/255459cede9341e39436ec8866d3fb65)](https://www.codacy.com/manual/akamhy/waybackpy?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=akamhy/waybackpy&amp;utm_campaign=Badge_Grade)
[![Maintainability](https://api.codeclimate.com/v1/badges/942f13d8177a56c1c906/maintainability)](https://codeclimate.com/github/akamhy/waybackpy/maintainability)
[![CodeFactor](https://www.codefactor.io/repository/github/akamhy/waybackpy/badge)](https://www.codefactor.io/repository/github/akamhy/waybackpy)
[![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/)
[![pypi](https://img.shields.io/pypi/v/waybackpy.svg)](https://pypi.org/project/waybackpy/)
![PyPI - Python Version](https://img.shields.io/pypi/pyversions/waybackpy?style=flat-square)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/akamhy/waybackpy/graphs/commit-activity)
![Repo size](https://img.shields.io/github/repo-size/akamhy/waybackpy.svg?label=Repo%20size&style=flat-square)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/akamhy/waybackpy/blob/master/LICENSE)

![Wayback Machine](https://raw.githubusercontent.com/akamhy/waybackpy/master/assets/waybackpy-colored%20284.png)

Waybackpy is a Python library that interfaces with [Internet Archive](https://en.wikipedia.org/wiki/Internet_Archive)'s [Wayback Machine](https://en.wikipedia.org/wiki/Wayback_Machine) API. Archive webpages and retrieve archived webpages easily.

Table of contents
=================
<!--ts-->

* [Installation](#installation)

* [Usage](#usage)
  * [As a Python package](#as-a-python-package)
    * [Saving an url](#capturing-aka-saving-an-url-using-save)
    * [Retrieving the oldest archive](#retrieving-the-oldest-archive-for-an-url-using-oldest)
    * [Retrieving the recent most/newest archive](#retrieving-the-newest-archive-for-an-url-using-newest)
    * [Retrieving archive close to a specified year, month, day, hour, and minute](#retrieving-archive-close-to-a-specified-year-month-day-hour-and-minute-using-near)
    * [Get the content of webpage](#get-the-content-of-webpage-using-get)
    * [Count total archives for an URL](#count-total-archives-for-an-url-using-total_archives)
    * [List of URLs that Wayback Machine knows and has archived for a domain name](#list-of-urls-that-wayback-machine-knows-and-has-archived-for-a-domain-name)

  * [With the Command-line interface](#with-the-command-line-interface)
    * [Save](#save)
    * [Oldest archive](#oldest-archive)
    * [Newest archive](#newest-archive)
    * [Total archives](#total-number-of-archives)
    * [Archive near specified time](#archive-near-time)
    * [Get the source code](#get-the-source-code)
    * [Fetch all the URLs that the Wayback Machine knows for a domain](#fetch-all-the-urls-that-the-wayback-machine-knows-for-a-domain)

* [Tests](#tests)

* [Dependency](#dependency)

* [Packaging](#packaging)

* [License](#license)

<!--te-->

## Installation

Using [pip](https://en.wikipedia.org/wiki/Pip_(package_manager)):

```bash
pip install waybackpy
```

or direct from this repository using git.

```bash
pip install git+https://github.com/akamhy/waybackpy.git
```

## Usage

### As a Python package

#### Capturing aka Saving an url using save()

```python
import waybackpy

new_archive_url = waybackpy.Url(

    url = "https://en.wikipedia.org/wiki/Multivariable_calculus",
    user_agent = "Mozilla/5.0 (Windows NT 5.1; rv:40.0) Gecko/20100101 Firefox/40.0"

).save()

print(new_archive_url)
```

```bash
https://web.archive.org/web/20200504141153/https://github.com/akamhy/waybackpy
```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPySaveExample></sub>

#### Retrieving the oldest archive for an URL using oldest()

```python
import waybackpy

oldest_archive_url = waybackpy.Url(

    "https://www.google.com/",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.8; rv:40.0) Gecko/20100101 Firefox/40.0"
).oldest()

print(oldest_archive_url)
```

```bash
http://web.archive.org/web/19981111184551/http://google.com:80/
```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyOldestExample></sub>

#### Retrieving the newest archive for an URL using newest()

```python
import waybackpy

newest_archive_url = waybackpy.Url(

    "https://www.facebook.com/",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.10; rv:39.0) Gecko/20100101 Firefox/39.0"

).newest()

print(newest_archive_url)
```

```bash
https://web.archive.org/web/20200714013225/https://www.facebook.com/
```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyNewestExample></sub>

#### Retrieving archive close to a specified year, month, day, hour, and minute using near()

```python
from waybackpy import Url

user_agent = "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.10; rv:38.0) Gecko/20100101 Firefox/38.0"
github_url = "https://github.com/"


github_wayback_obj = Url(github_url, user_agent)

# Do not pad (don't use zeros in the month, year, day, minute, and hour arguments). e.g. For January, set month = 1 and not month = 01.
```

```python
github_archive_near_2010 = github_wayback_obj.near(year=2010)
print(github_archive_near_2010)
```

```bash
https://web.archive.org/web/20100719134402/http://github.com/
```

```python
github_archive_near_2011_may = github_wayback_obj.near(year=2011, month=5)
print(github_archive_near_2011_may)
```

```bash
https://web.archive.org/web/20110519185447/https://github.com/
```

```python
github_archive_near_2015_january_26 = github_wayback_obj.near(
    year=2015, month=1, day=26
)
print(github_archive_near_2015_january_26)
```

```bash
https://web.archive.org/web/20150127031159/https://github.com
```

```python
github_archive_near_2018_4_july_9_2_am = github_wayback_obj.near(
    year=2018, month=7, day=4, hour = 9, minute = 2
)
print(github_archive_near_2018_4_july_9_2_am)
```

```bash
https://web.archive.org/web/20180704090245/https://github.com/

```

<sub>The library doesn't supports seconds yet. You are encourged to create a PR ;)</sub>

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyNearExample></sub>

#### Get the content of webpage using get()

```python
import waybackpy

google_url = "https://www.google.com/"

User_Agent = "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2454.85 Safari/537.36"

waybackpy_url_object = waybackpy.Url(google_url, User_Agent)


# If no argument is passed in get(), it gets the source of the Url used to create the object.
current_google_url_source = waybackpy_url_object.get()
print(current_google_url_source)


# The following chunk of code will force a new archive of google.com and get the source of the archived page.
# waybackpy_url_object.save() type is string.
google_newest_archive_source = waybackpy_url_object.get(
    waybackpy_url_object.save()
)
print(google_newest_archive_source)


# waybackpy_url_object.oldest() type is str, it's oldest archive of google.com
google_oldest_archive_source = waybackpy_url_object.get(
    waybackpy_url_object.oldest()
)
print(google_oldest_archive_source)
```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyGetExample#main.py></sub>

#### Count total archives for an URL using total_archives()

```python
import waybackpy

URL = "https://en.wikipedia.org/wiki/Python (programming language)"

UA = "Mozilla/5.0 (iPad; CPU OS 8_1_1 like Mac OS X) AppleWebKit/600.1.4 (KHTML, like Gecko) Version/8.0 Mobile/12B435 Safari/600.1.4"

archive_count = waybackpy.Url(
    url=URL,
    user_agent=UA
).total_archives()

print(archive_count) # total_archives() returns an int
```

```bash
2440
```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyTotalArchivesExample></sub>

####  List of URLs that Wayback Machine knows and has archived for a domain name

1) If alive=True is set, waybackpy will check all URLs to identify the alive URLs. Don't use with popular websites like google or it would take too long.
2) To include URLs from subdomain set sundomain=True

```python
import waybackpy

URL = "akamhy.github.io"
UA = "Mozilla/5.0 (iPad; CPU OS 8_1_1 like Mac OS X) AppleWebKit/600.1.4 (KHTML, like Gecko) Version/8.0 Mobile/12B435 Safari/600.1.4"

known_urls = waybackpy.Url(url=URL, user_agent=UA).known_urls(alive=True, subdomain=False) # alive and subdomain are optional.

print(known_urls) # known_urls() returns list of URLs
```

```bash
['http://akamhy.github.io',
'https://akamhy.github.io/waybackpy/',
'https://akamhy.github.io/waybackpy/assets/css/style.css?v=a418a4e4641a1dbaad8f3bfbf293fad21a75ff11',
'https://akamhy.github.io/waybackpy/assets/css/style.css?v=f881705d00bf47b5bf0c58808efe29eecba2226c']
```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyKnownURLsToWayBackMachineExample#main.py></sub>

### With the Command-line interface

#### Save

```bash
$ waybackpy --url "https://en.wikipedia.org/wiki/Social_media" --user_agent "my-unique-user-agent" --save
https://web.archive.org/web/20200719062108/https://en.wikipedia.org/wiki/Social_media
```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyBashSave></sub>

#### Oldest archive

```bash
$ waybackpy --url "https://en.wikipedia.org/wiki/SpaceX" --user_agent "my-unique-user-agent" --oldest
https://web.archive.org/web/20040803000845/http://en.wikipedia.org:80/wiki/SpaceX
```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyBashOldest></sub>

#### Newest archive

```bash
$ waybackpy --url "https://en.wikipedia.org/wiki/YouTube" --user_agent "my-unique-user-agent" --newest
https://web.archive.org/web/20200606044708/https://en.wikipedia.org/wiki/YouTube
```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyBashNewest></sub>

#### Total number of archives

```bash
$ waybackpy --url "https://en.wikipedia.org/wiki/Linux_kernel" --user_agent "my-unique-user-agent" --total
853

```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyBashTotal></sub>

#### Archive near time

```bash
$ waybackpy --url facebook.com --user_agent "my-unique-user-agent" --near --year 2012 --month 5 --day 12
https://web.archive.org/web/20120512142515/https://www.facebook.com/
```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyBashNear></sub>

#### Get the source code

```bash
waybackpy --url google.com --user_agent "my-unique-user-agent" --get url # Prints the source code of the url
waybackpy --url google.com --user_agent "my-unique-user-agent" --get oldest # Prints the source code of the oldest archive
waybackpy --url google.com --user_agent "my-unique-user-agent" --get newest # Prints the source code of the newest archive
waybackpy --url google.com --user_agent "my-unique-user-agent" --get save # Save a new archive on wayback machine then print the source code of this archive.
```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackPyBashGet></sub>

####  Fetch all the URLs that the Wayback Machine knows for a domain
1) You can add the '--alive' flag to only fetch alive links.
2) You can add the '--subdomain' flag to add subdomains.
3) '--alive' and '--subdomain' flags can be used simultaneously.
4) All links will be saved in a file, and the file will be created in the current working directory.

```bash
pip install waybackpy

# Ignore the above installation line.

waybackpy --url akamhy.github.io --user_agent "my-user-agent" --known_urls 
# Prints all known URLs under akamhy.github.io


waybackpy --url akamhy.github.io --user_agent "my-user-agent" --known_urls --alive 
# Prints all known URLs under akamhy.github.io which are still working and not dead links.


waybackpy --url akamhy.github.io --user_agent "my-user-agent" --known_urls --subdomain 
# Prints all known URLs under akamhy.github.io inclusing subdomain


waybackpy --url akamhy.github.io --user_agent "my-user-agent" --known_urls --subdomain --alive 
# Prints all known URLs under akamhy.github.io including subdomain which are not dead links and still alive.

```

<sub>Try this out in your browser @ <https://repl.it/@akamhy/WaybackpyKnownUrlsFromWaybackMachine#main.sh></sub>

## Tests

[Here](https://github.com/akamhy/waybackpy/tree/master/tests)

## Dependency

None, just python standard libraries (re, json, urllib, argparse and datetime). Both python 2 and 3 are supported :)

## Packaging

1. Increment version.

2. Build package ``python setup.py sdist bdist_wheel``.

3. Sign & upload the package ``twine upload -s dist/*``.

## License

Released under the MIT License. See
[license](https://github.com/akamhy/waybackpy/blob/master/LICENSE) for details.
