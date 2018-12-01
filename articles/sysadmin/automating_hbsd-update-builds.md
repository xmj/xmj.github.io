Automating HardenedBSD update builds
====================================

In this tutorial I show you how to automate HardenedBSD update builds on a
build server, publish them automatically, and fetch them on clients
as needed.

# Ingredients:

- Recent HardenedBSD installation
- hbsd-update-build (in base)
- Your own KERNCONF
- update-publisher repository
- nginx

# Preparation

Make sure you are running a somewhat recent HardenedBSD installation.  For the
sake of this exercise, we will build updates using the `HARDENEDBSD-MINIMAL`
kernel config [1].

Shawn Webb has automated quite a lot of the steps around building updates with
`hbsd-update-build`, which you can find in the update-publisher repository from
GitHub. These scripts are written in zshell, so let's install that and check
out the repository.

```
    pkg install -y zsh git
    git clone https://github.com/hardenedbsd/update-publisher.git
```

Inside of the `update-publisher` directory, you can find actively used examples
in `configs/`, libraries used for building in `lib/`, and two scripts in the
directory root.

# Building HardenedBSD

First, we will generate a file `configs/hardenedbsd-amd64-minimal.json` based
on the following snippet:

```
{
        "builds": [
                {
                        "name": "master",
                        "enabled": true,
                        "repo": "git://github.com/HardenedBSD/hardenedBSD.git",
                        "branch": "hardened/current/master",
                        "kernels": "HARDENEDBSD-MINIMAL",
                        "want_chroot_build": 1
                        "unsigned": 1,
                        "devmode": "yes",
                        "publish": [
                                {
                                        "method": "cp",
                                        "directory": "/path/to/some/local/zfs/dataset/"
                                }
                        ]

                }
        ]
}
```

The variables used above require some explanation. As the JSON contains a list of
builds, the name will be what identifies the build on the console. Disabling it
will skip the build.  `repo` and `branch` are used by git to determine where
you download from and which branch you check out. `kernels` selects the
kernels to build. `want_chroot_build` makes sure git gets checked out to
/usr/src (or at least will be pulled if a repository is found already) and that
it is built before distributing it into the chroot. This takes twice as long
but ensures consistency.

Armed with this config file, we can finally start a build.

```
    zsh run.sh -c configs/hardenedbsd-amd64-minimal.json
```

This might take a while as our config above yields two full builds. Go fetch
yourself a nice coffee, head to the library, checkout a few books, read them
and return back.

# Distributing HardenedBSD updates

XXX: Write about setting up nginx in a jail, jailing the zfs dataset used above

# Updating HardenedBSD

XXX: Create `hbsd-update.conf` that works with those settings

XXX: `hbsd-update -U -d -c hbsd-update.conf`

[1] https://github.com/hardenedbsd/hardenedbsd/blob/hardened/current/master/sys/amd64/conf/HARDENEDBSD-MINIMAL
