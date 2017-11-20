Speeding up  builds on FreeBSD
==============================

If you're repeatedly building components of the FreeBSD operating system - kernel, base or userland - you will be interested in optimizing the build duration. Luckily, over time the various commercial users of FreeBSD have figured out various ways of speeding up that build process. The probably most obvious way of shaving off time is through to not rebuild things that have not changed. 
In this article I'd like to show a few ways of achieving this from a user's perspective.


METAMODE
--------

For kernel/base builds, one way of achieving this is using meta mode. This makes make(1) capture information that will be relevant for next builds in a .meta file, such as the compiler invocation, files read during compile (including includes, and their location), libraries used, interesting syscalls issued, etc. make(1) achieves that by using the filemon(4) interface (required for e.g. tracing syscalls issued during make(1) execution). On subsequent runs, if a .meta file can be found, make(1) determines if the information in this .meta file still contains uptodate information (e.g. by comparing the proposed to the past compiler invocation), comparing access times for libraries and code used to the object previously built), and if not, rebuilds the object.

Metamode can be used by setting the following in `/etc/src-env.conf`:

```
WITH_META_MODE=YES
```

Using metamode I've rebuilt `HardenedBSD 12.0-CURRENT world/kernel` on a ThinkPad x260 within under ten minutes.

DIRDEPS
-------

Using dirdeps leverages the metadata built using make(1)'s metamode. Information present in the so built .meta files can be used to derive a dependency graph, such that there is a way of (taking the example of bin/sh) building not only sh(1) but also its dependencies (in this case, libc, libcompiler_rt, libedit, libncursesw, etc). This feature then is used to derive a full graph of the source tree, and not traverse it unnecessarily by building things in the right order.

Dirdeps can be enabled by setting the following in `/etc/src-env.conf`:

```
WITH_DIRDEPS_BUILD=yes
```

Setting this implies various other options, including the above-mentioned metamode, automatic build of objdirs, staging install to a test directory, etc. Note that its main use is for quickly being able to test changes on a running system, and as such may be more useful for development.

POUDRIERE and CCACHE
--------------------

If you have previously built and maintained a repository using poudriere, you will hopefully have noticed that it by default rebuilds thigns only when necessary - for example in the case of version updates, shlib bumps of dependencies, change of selected options. But even so, recompilation of previously built ports can be further increased by using ccache(1), which caches compilation results (not just result metadata). 

```
pkg install ccache
```

Within poudriere you can enable this feature by setting `CCACHE_DIR=/path/to/ccache/dir` in `poudriere.conf`, and, if that directory does not exist, creating it. Optionally you can store a config file `ccache.conf` in it, setting limits to the maximum cache size (5G by default) and many more.

POUDRIERE + CCACHE + MEMCACHED
------------------------------

If your package build box is among the more beefier variants (no, my ThinkPad won't quite do) it may be worthwile to using memcached to store previous compilation's output. 

If you have previously installed ccache and poudriere, `pkg delete` both and replace them with `poudriere-devel` (3.1.99.20170310 or later), and `ccache-memcached-static`. At the time of writing, the latest poudriere release has not yet obtained the necessary ccache enhancements, and static ccache is required for it to work in buildjails without obtaining circular dependencies with libmemcached.

Then, within `poudriere.conf` additionally set the following:

```
CCACHE_STATIC_PREFIX=/usr/local
RESTRICT_NETWORKING=no
```

If you have not done this in the previous step, create a ccache.conf, and add these two lines:

```
memcached_conf = --SERVER=localhost:11211
memcached_only = true
```

Last but not least, execute the following to enable and start memcached:

```
# sysrc memcached_enable=YES
# sysrc memcached_flags="-l localhost -m $megabytes"
# service memcached start
```

Adjust the amount of megabytes to whatever your buildbox supports, and start a bulk run to get things going.

KERNEL + BASE + CCACHE + MEMCACHE
---------------------------------

With builtin support for ccache(1) within the FreeBSD base build system, the next step is to leverage above configuration by enabling `WITH_CCACHE_BUILD=yes` in `src.conf`, and using metamode, dirdeps, ccache and memcached together.



ADDITIONAL READING
------------------
- The original METAMODE talk given by sjg during BSDCan 2011:
  [http://www.crufty.net/sjg/blog/BuildingBSD.pdf](http://www.crufty.net/sjg/blog/BuildingBSD.pdf).
- ccache.conf(5) lists various options that could be used to tune/adjust ccache behavior.
- memcached(1) lists options that could be used to enable (SASL) authentication.
