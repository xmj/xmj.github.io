Turning FreeBSD to HardenedBSD
==============================

In this tutorial I show you how to turn `FreeBSD 11.0-RELEASE` into
`HardenedBSD`'s `11-STABLE` build that ships with `LibreSSL`.

# Ingredients:

* Recent FreeBSD installation
* unbound
* hbsd-update (from Github)
* HardenedBSD update certificates (from Github)


# Preparation

Make sure you are running a supported FreeBSD version. Otherwise, bad things
will happen. Now is *also* the time to do backups (and by this I mean not just
a recursive zfs snapshot but actual backups).

In a first step, we will install `unbound` and `ca_root_nss`. The former,
because the current maintainer of base unbound is [not
willing](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=211507) to provide
an easy way of doing DNSSEC validation without additional steps; the latter,
because it eliminates HTTPS verification errors with fetch(1) later in this
tutorial.

```
    # pkg install unbound ca_root_nss
```

In a next step, we download the latest `hbsd-update` shellscript from
HardenedBSD's git repository, the corresponding config file, and certificates.
Once fetched into a temporary folder, we modify the `hbsd-update` script to
take into account the ports unbound install, and move the files into their
final destination.

```
    % cd /tmp
    % fetch https://raw.githubusercontent.com/HardenedBSD/hardenedBSD/hardened/11-stable/master-libressl/{usr.sbin/hbsd-update/hbsd-update,etc/hbsd-update.conf,share/keys/hbsd-update/trusted/ca.hardenedbsd.org,share/keys/hbsd-update/trusted/dnssec.key-2016-07-30}
    % sed -i -e '/^UNBOUND_HOST=/ s/\/usr\/sbin\/unbound-host/\/usr\/local\/sbin\/unbound-host/' hbsd-update
    % chmod +x hbsd-update

    % sudo -i

    # mv hbsd-update /usr/sbin
    # mv hbsd-update.conf /etc
    # mkdir -p /usr/share/keys/hbsd-update/trusted
    # mv ca.hardenedbsd.org /usr/share/keys/hbsd-update/trusted
    # mv dnssec.key-2016-07-30 /usr/share/keys/hbsd-update/trusted
    # ln -s /usr/share/keys/hbsd-update/trusted/ca.hardenedbsd.org /usr/share/keys/hbsd-update/trusted/5905e1b4.0
    # ln -s /usr/share/keys/hbsd-update/trusted/dnssec.key /usr/share/keys/hbsd-update/trusted/dnssec.key-2016-07-30
```

Now with the preparation out of the way, we can get to the meat:

# Deploying HardenedBSD

You may have already guessed: we will use `hbsd-update` to turn FreeBSD into
HardenedBSD and reboot once that's done.

```
    # hbsd-update && reboot
```

NB: If you've checked out the FreeBSD source code to `/usr/src`, append the
`-s` flag to have hbsd-update extract the HardenedBSD sources in-place. Do make
sure to remove corresponding vcs directories like .svn or .git.

```
    # rm -rf /usr/src/{.svn,.git,*}
    # hbsd-update -s && reboot
```

Finally, you'll notice that many of your installed third-party tools are now
perfectly unusable, having been compiled for OpenSSL while we're using
LibreSSL. You'll start fixing this by reinstalling `pkg`, and upgrading every
installed package.

```
    # pkg-static install pkg
    # pkg upgrade -f
```

You'll also find that this leads to the caveat that all the packages you have
installed from ports are now missing shared libraries, and need to be
reinstalled.

If you've installed any of those third-party tools from ports, you will want to
reinstall them using the HardenedBSD ports tree.

To make full use of HardenedBSD's security features, install secadm and
secadm-kmod, and take a look at secadm-rules the HBSD project provides:

```
    % git clone https://github.com/hardenedbsd/hardenedbsd-ports ports
    % make -C ports/hardenedbsd/secadm config install clean
    % make -C ports/hardenedbsd/secadm-kmod config install clean
    % git clone https://github.com/HardenedBSD/secadm-rules
```

At this point, I'd like to point out to the
[HardenedBSD Handbook](https://hardenedbsd.org/~shawn/hbsd_handbook/book.html#hardenedbsd-secadm)
chapter on `secadm`, and call it a day.
