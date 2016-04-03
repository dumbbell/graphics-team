+++
title = "Migrating xorg-dev to Git"
date = "2014-10-19T20:10:00+01:00"
author = "Jean-Sébastien Pédron"

#featured = "logo-git.png"
#featuredpath = "/images"

categories = [ "The Ports tree" ]
toc = false
+++

We are experimenting with Git to replace the ["xorg-dev” Subversion
repository](https://wiki.freebsd.org/Graphics#Development_repository).

Remember, this repository is used to work on the graphics stack ports
before they go to the official Ports tree. For instance, this is where
we worked on the update to Mesa 10.3.0. Now, that Mesa 10.3.0 is
committed, xorg-dev contains Mesa 10.3.1.

<!--more-->

xorg-dev is a Subversion repository containing only the ports and
infrastructure Makefiles which differ from the official Ports tree. The
current workflow simply consists of:

1. prepare a new port or update in xorg-dev's trunk
2. when ready, copy the files in a Ports tree working copy
3. remove the obsolete files
4. commit the change in the Ports tree
5. optionally, remove the committed work from xorg-dev

A nice advantage is that xorg-dev remains lighweight. This makes svn
commands fast.

But problems arise when there are changes committed directly to the
Ports tree. We must be careful to bring those changes to xorg-dev but
from time to time, we fail to do so and they are lost. Furthermore, it's
very hard to track history between xorg-dev and the official Ports tree.

That's why we want to change this workflow and switch to a complete Git
clone of the Ports tree.

There's already a [Git mirror of the Ports tree](https://github.com/freebsd/freebsd-ports)
available on GitHub. We are going to use this as our upstream repository
and create another repository, called [`freebsd-ports-graphics` on
GitHub](https://github.com/freebsd/freebsd-ports-graphics):
this is going to be the new xorg-dev.

This will allow us to:

* have a full Ports tree, so it's easier to test: no need to merge
  anything to `/usr/ports`
* handle conflicts during the developments, not when we want to commit
  the final patch
* keep the history in a single place
* accept GitHub pull requests from anyone (not discussed yet)

We'll try to use topic branches too (eg. a branch for xorg-server 1.14,
another one for Mesa 10.3.1 and so on), though this is subject to
change.

The [workflow is described on the wiki](https://wiki.freebsd.org/Graphics/Ports_development_workflow).

Once the experiment concludes, we'll inform you about our decision to
either keep Subversion or move to Git.
