# Details
This repository contains the original/classic FreeBSD `fortune(6)`
datfiles, including offensives (`fortune -o`), which were present in
FreeBSD until roughly November 13, 2017.

These files are direct copies from the FreeBSD repository, immediately
prior to their removal in r325781 / git 0271df5.

# Files

```
fortunes
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

# Building

Use of `strfile(8)` is required to create a .dat file for each respective
fortune.  Use of the `-C` flag is a requirement.  Then, the combination
of both the non-dat and .dat file must be placed in the `fortune(6)`
directory search path (see `fortune -l`).  I do not know the use of the
`.sp.ok` files, though they look related to spell/ispell.

# History
The below applies to FreeBSD HEAD (a.k.a. CURRENT, i.e. FreeBSD 12.x as of
this writing).  However, the below commits are intended to be MFC'd (i.e.
merged into stable/11 (FreeBSD 11.x) and stable/19 (FreeBSD 10.x)).

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
mailing list post should read every single reply in the thread, as there is
some factual and contextually relevant details pertaining to the intentions
of said quotes.

