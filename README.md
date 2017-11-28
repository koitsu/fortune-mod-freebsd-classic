# Details

This repository contains the original/classic FreeBSD `fortune(6)`
datfiles, including offensives (`fortune -o`), which were present in
FreeBSD until roughly November 13, 2017.

These files are direct copies from the FreeBSD repository, immediately
prior to their removal in r325781 / git 0271df5.

# Files

```
fortunes
fortunes-o
fortunes-o.sp.ok
fortunes.sp.ok
gerrold.limerick
limerick
limerick.sp.ok
murphy
murphy-o
murphy.sp.ok
startrek
startrek.sp.ok
zippy
zippy.sp.ok
```
# Common Use

I will soon be submitting a new FreeBSD port called
`misc/fortune-mod-freebsd-classic` which will install these classic
datfiles for use.  No other changes need be done, as `fortune(6)`
searches for files in both `/usr/share/games/fortune` as well as
`/usr/local/share/games/fortune` (ports/pkgs install theirs in the
latter).

# Building

Use of `strfile(8)` is required to create a .dat file for each
respective fortune.  Use of the `-C` flag is a requirement.  Then, the
combination of both the non-dat and .dat file must be placed in the
`fortune(6)` directory search path.

Use of the environment variable `FORTUNE_PATH` can also be used, but I
found it to be quirky; things like
`FORTUNE_PATH=/path/to/dir fortune murphy` would regularly output
nothing for no reason I could determine.

I don't know the purpose of the `.sp.ok` files, though they look
potentially related to classic spell/ispell.

# History

The below applies to FreeBSD HEAD (a.k.a. CURRENT, i.e. FreeBSD 12.x as of
this writing).  However, the below commits are intended to be MFC'd (i.e.
merged into stable/11 (FreeBSD 11.x) and stable/10 (FreeBSD 10.x)).

On November 13 2017 at ~21:55 UTC,
[FreeBSD Port Management Team](https://www.freebsd.org/administration.html#t-portmgr)
member Mark Felder (feld) removed all "fortune quotes attributed to or
providing admiration of Adolf Hitler" from the `fortunes` file.

A day later, on November 14 2017 at ~21:30 UTC,
[FreeBSD Core Team](https://www.freebsd.org/administration.html#t-core)
member Benno Rice (benno) removed all the fortune datfiles, excluding
`freebsd-tips` and `freebsd-tips.dat`.  All removed files were
subsequently added to `ObsoleteFiles.inc` (i.e. will be removed during
`make delete-old`).

Commits:

* [r325781](https://svnweb.freebsd.org/base?view=revision&revision=325781) / [git 0271df5](https://github.com/freebsd/freebsd/commit/0271df5714d9ce5274f82889febb6536a2fdba59)
* [r325828](https://svnweb.freebsd.org/base?view=revision&revision=325828) / [git a7833d5](https://github.com/freebsd/freebsd/commit/a7833d533faa497dfc14b6873380ecad33b19f04)
* [r325829](https://svnweb.freebsd.org/base?view=revision&revision=325829) / [git dfae4e4](https://github.com/freebsd/freebsd/commit/dfae4e4a6521a6fd13d1a1b94932f4ed63df3d01)

r325828 resulted in
[a brief discussion](https://lists.freebsd.org/pipermail/svn-src-all/2017-November/thread.html#153749)
on the FreeBSD mailing list svn-src-all:

* Rodney W. Grimes (rgrimes) [cited the need for r325829](https://lists.freebsd.org/pipermail/svn-src-all/2017-November/153755.html)
* Cy Schubert (cy) [proposed removing fortune altogether](https://lists.freebsd.org/pipermail/svn-src-all/2017-November/153787.html)
* Jeremie Le Han (jlh) [asked for justification](https://lists.freebsd.org/pipermail/svn-src-all/2017-November/153773.html), particularly where this was discussed and the "why" behind it

The only response was to the latter, where Rice stated, quote,
["it was raised to core but I decided to take unilateral action"](https://lists.freebsd.org/pipermail/svn-src-all/2017-November/153779.html),
adding that the removal was based on his "discovery of quotes from Adolf
Hitler in the file", "trying to be the editors humour is not something
we're really cut out for and that we should get out of the game", and
that "personally I feel that this is the kind of thing that doesn't
need to live on".  There was no mention or comment from Felder.

The removal of said quotes, and said fortunes, was
[more extensively discussed](http://mail-index.netbsd.org/current-users/2017/11/18/msg032672.html)
on the NetBSD current-users mailing list.  Readers of the aforementioned
mailing list post should read every single reply in the thread, as there
is some factual and contextually relevant details pertaining to the
intentions of said quotes.

# Older History

Removal of "political propaganda" (specifically, Rush Limbaugh quotes)
from `fortunes-o.real` was done on February 5 2013 at ~14:39 UTC by
Dag-Erling Smorgrav (des).  Removal was done in commit r246362.

fortunes-o and its related bits were removed entirely from FreeBSD on
March 12 2013 at ~12:35 UTC by John H. Baldwin (jhb).  The commit
message implies there was a discussion about this amongst the FreeBSD
Core Team.  Removal was done in commit r248200.

Commits:

* [r246362](https://svnweb.freebsd.org/base?view=revision&revision=246362) / [git 72c8e2d](https://github.com/freebsd/freebsd/commit/72c8e2de5282a2d1848447691f49c30e83e28950)
* [r248200](https://svnweb.freebsd.org/base?view=revision&revision=248200) / [git 369cfc7](https://github.com/freebsd/freebsd/commit/369cfc7386b7e6ca0efa2c406063e75210ab5fa2)

Prior to their removal, the way `fortunes-o` and `fortunes-o.dat` were
created was (to me) quite amusing:

1. fortunes-o was created by essentially piping fortunes-o.real
through `tr(1)` to rot13 its content (fortunes-o.real in the svn/cvs
repository itself was in readable plain-text),

2. fortunes-o.dat was created from the aforementioned fortunes-o file
while using the `-x` flag to `strfile(8)`, which causes `fortune` to
rot13 the quote, "decoding" it before being shown.

Best I can tell, the above two steps were done solely to keep plain-text
"offensive words" from being stored in plain-text on a users'
filesystem.

There was also a file called `fortunes-o.fake`, which contained nothing
more than content informing the user that "offensive" fortunes were
essentially disabled.  The FreeBSD fortune Makefile could essentially
could be modified in-place through `sed(1)` during the build phase, to
change `TYPE=real` into `TYPE=fake`, thus making `fortune -o` output
said comment:

* [fortunes-o.fake](https://svnweb.freebsd.org/base/head/games/fortune/datfiles/fortunes-o.fake?revision=2491&view=markup&pathrev=248199)
* [fortune Makefile](https://svnweb.freebsd.org/base/head/games/fortune/datfiles/Makefile?revision=174426&view=markup&pathrev=288484)

