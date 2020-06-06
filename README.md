This displays a sorted list of a repository's forks' updated times.

It caches the pages to reduce github API hits.

## Features
* Caches the pages (initial repository page and the json forks)

## Dependencies
* curl installed and in the path
* ...and a bunch of perl packages (see the Debian section)

### Debian
* libdatetime-format-iso8601-perl
* liblist-allutils-perl # We use List::Util
* libfile-homedir-perl  # To spy on you (or to find a place to store the config file)
* libconfig-simple-perl
* libtext-table-perl
* others I've now added; see them at the top of the script

## Setup
* You'll want to to set up an auth token. See:
	* https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line#using-a-token-on-the-command-line
	* (Without the github token your api calls will be much more limited)

### Reliability
* I didn't use Github's API for the initial page hit (listing of all forks), I just get the HTML with curl. Sorry.
* Using the API and the JSON data to get the forks would be preferable and more future-compatible -- also less error-prone since I'm relying on potentially-changing HTML. That'll be an easy change, and we receive the json for the fork along with all the others anyway, but I've just not implemented that yet.

### New
* Commandline options now added, including:
	* --clapi (clear bad (zero size) cache entries)
	* See --help and the script for more

### Other
* Aside from the stuff in Setup, deleting cache must be done by hand.
  * --clapi can clear 0-length entries, but to remove the rest... manually.
* This is in perl
* I experimented with indentation for code-readability. :}
* I'm not using perl's HTTP modules -- I'm calling curl directly for now. Sorry.
* This uses forward slashes for local file paths
* Also, it uses /tmp/github-forks-cache/ if no cache\_dir is specified in the config
* Probably not necessary to mention, but in some places I separate the github username from the repo with double underscore (__). I'm not sure if this can result in a name collision, if, say, a username or repo has a double-underscore in it.

### Example configuration options (config file created with --init)
* github_user
* github_token
* cache_dir (defaults to /tmp/github-forks-cache)
