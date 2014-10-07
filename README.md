# http://bl.ocks.org Skeletons

This Rakefile simply creates and initialises new gists suitable for fancy
display via the rather wonderful http://bl.ocks.org gist viewer.

It's not very generic - it assumes I'm running it - but it should be simple to
modify it to work for yourself.

Basic use:

    rake default["Block Description"]

This will create a new gist with the description `"Block Description"` and
store it locally in `mnem/raw/<gist id>`. After that, just update the gist
as you would normally with `git`.

The structure of the skeleton has been pulled from:
[http://bost.ocks.org/mike/block/](http://bost.ocks.org/mike/block/).

Oh, and the `Rakefile` requires you to have these command line tools installed:

- `curl` - [http://curl.haxx.se]()
- `git` - [http://git-scm.com]()
- `node` - [http://nodejs.org]()
- `gistup` - Install with `npm`: `npm install --global gistup`

There's a reasonable chance you need `ruby` >= 1.9.3 too - I think the dirty
hack I use to stop mkmf log files being spewed out requires that for `File::NULL`.
And it'll probably break at some random future date when the mkmf library changes.
