# Welcome to the SlackOnly software repository!

SlackOnly is a third party software repository for Slackware Linux that
provides binary packages built from [SlackBuilds.org][1] build scripts.
The goal is to enable users to install any package from
[SlackBuilds.org][1] using pre-compiled binary packages. SlackOnly
packages contain Metadata that provides dependency information to
package managers that have the ability to read such information.
SlackOnly assumes that its users are running a full installation of
Slackware Linux prior to use.

SlackOnly supports the following Slackware releases and architectures:

 * Slackware 14.1 32 bit [14.1-x86][2]
 * Slackware 14.1 64 bit [14.1-x86_64][3]
 * Slackware 14.2 32 bit [14.2-x86][4]
 * Slackware 14.2 64 bit [14.2-x86_64][5]

Links to each repository are in the footer of this document.

## How to use SlackOnly

There is a variety of package managers that will enable you to use
SlackOnly on your Slackware installation.

 * slackpkg with the slackpkg+ extension
 * slpkg
 * slapt-get and the gslapt GUI

Below are the descriptions and directions explaining how to install each
of these package managers.  Also included in the directions are the
configuration changes necessary to use each package manager with SlackOnly.

#### Slackpkg with Slackpkg+

    Slackpkg is included in default installations of the Slackware Linux
    distribution.  Slackpkg+ is an extension of slackpkg that allows
    the use of third party repositories.  Many users like slackpkg+ over
    other third party software management options.  This preference is
    due to the fact that slackpkg allows users to continue to use the
    same slackpkg commands that are familiar.  This package manager, and
    its extension slackpkg+, do not offer automatic dependency
    resolution as a feature.

1.  First, download slackpkg+ and install it as root by running the
    "installpkg" command.

    It can be downloaded [here](https://sourceforge.net/projects/slackpkgplus/files/).

    > root@localhost:~# installpkg slackpkg+*.t?z

2.  Next, edit /etc/slackpkg/slackpkgplus.conf. Edit the REPOPLUS
    variable and add a new SlackOnly MIRRORPLUS variable:

    > REPOPLUS=( slackpkgplus restricted alienbob slacky slackonly )

    > MIRRORPLUS['slackonly']=https://packages.slackonly.com/pub/packages/RELEASE-ARCH/

    RELEASE should be either "14.1" or "14.2" or "current" and ARCH should be
    either "x86" or "x86_64". You should use the same release and
    architecture as your Slackware installation. Adding the wrong
    values will cause problems with your installation.

3.  Finally, run the following commands as root to import the SlackOnly GPG
    key and to update the slackpkg cache with the SlackOnly package
    list.

    > root@localhost:~# slackpkg update gpg

    > root@localhost:~# slackpkg update

    You are now ready to use slackpkg with the slackpkg+ extension to
    access the SlackOnly repository of your choice.

*   Getting Help

    Further directions on how to use slackpkg can be found in the man
    page or online in the [slackpkg+ README](http://slakfinder.org/slackpkg+/src/README).


#### Slpkg

    Slpkg is a stand-alone command line package manager.  It
    automatically computes dependencies,  Slpkg enables the user to
    install, update, remove packages and their dependencies with just a
    few commands.  Slpkg distinguishes itself from other package
    managers by its user friendliness and great documentation.  It
    offers features like dependency resolution, colorful output, better
    security, faster processing, amongst other features.

1.  First, download and install the latest release of slpkg.  There are
    a number of ways to get slpkg.  Python users can install slpkg using
    the "pip" command.  [SlackBuilds.org][1] users can run the "sbopkg"
    command to install slpkg.  To install from source, refer to the
    slpkg README for more information.  A binary package can be
    downloaded from the slpkg home page and be installed with the
    "installpkg" command.

    The README can be found [here](https://gitlab.com/dslackw/slpkg/blob/master/README.rst).

    For simplicity we will download the binary package from the slpkg
    SourceForge page and install it as root using the "installpkg"
    command.

    The slpkg SourceForge page can be found [here](https://sourceforge.net/projects/slpkg/files/binary/).

    > root@localhost:~# installpkg slpkg*_dsw.t?z

2.  Next, edit /etc/slpkg/slpkg.conf and change the RELEASE variable to
    your Slackware release.  If you are using Stable Slackware there is
    nothing to change.

    > RELEASE=stable

3.  Following that, edit /etc/slpkg/repositories.conf and enable the
    SlackOnly repository by uncommenting the line with: "slonly"

    > slonly

4.  Finally, synchronize the package lists:

    > root@localhost:~# slpkg update

    You are now ready to start using slpkg to manage your SlackOnly
    binary packages.

*   Getting Help

    The slpkg help can be found on your system by running "slpkg -h" and
    in the man page by running "man slpkg".  The slpkg README can be
    found in the /usr/doc/slpkg-$VERSION directory on your system.  You
    can also view the [README online](https://gitlab.com/dslackw/slpkg/blob/master/README.rst).

#### Slapt-get

    slapt-get is an APT-like package management system for Slackware. It
    aims to emulate Debian's package manager (apt-get) as closely as
    possible.  It provides automatic dependency resolution and a
    companion graphical interface called gslapt.

1.  Download and install [slapt-get](https://software.jaos.org/#slapt-get).

    > root@localhost:~# installpkg slapt-get*.t?z

2.  Edit /etc/slapt-get/slapt-getrc and add:

    > SOURCE=https://packages.slackonly.com/pub/packages/RELEASE-ARCH/:DEFAULT

    RELEASE should be either "14.1" or "14.2" or "current" and ARCH should be
    either "x86" or "x86_64".  You should use the same release and
    architecture as your Slackware installation.  Adding the wrong
    values will cause problems with your installation.

3.  Next, import the SlackOnly GPG key:

    > root@localhost:~# slapt-get --add-keys

4.  Finally, update the package list cache for slapt-get:

    > root@localhost:~# slapt-get --update

    You are ready to start using slapt-get with the SlackOnly
    repository.

*   Getting Help

    You can access the slapt-get help by running "slapt-get -h".
    Additional help can be found by looking at the man page, "man
    slapt-get".  There is a FAQ included with the slapt-get package,
    located in /usr/share/doc/slapt-get-$VERSION.  Further inquiries can
    be found on the [slapt-get home page](https://software.jaos.org/).

#### Gslapt

    Gslapt is a GTK front-end for slapt-get.  It aims to streamline the
    package management process for slapt-get.  It is similar to the
    Synaptic GUI package manager seen in Debian Linux.

1.  Download and install [Gslapt](https://software.jaos.org/#gslapt):

    > root@localhost:~# installpkg gslapt*.t?z

2.  Launch Gslapt with root privileges.  This can be done directly by
    logging into the root account.  It can also be launched as a
    limitted user by by prefixing the "gslapt" command with kdesu.

    As root:
    > root@localhost:~# gslapt

    As a limitted user:
    > user@localhost:~$ kdesu gslapt

    You will be asked for the root account password if you use "kdesu".

*   Getting Help

    You can find additional documentation, as well as screenshots of
    Gslapt in action on the Gslapt home page.  On this page there
    is also a link to the slapt-get mailing list, which is also used for
    Gslapt.  As always you can find the README and FAQ files in
    /usr/share/doc/gslapt as well.

    The Gslapt home page can be found [here](https://software.jaos.org/).

---

## Development and Quality Control

*  See [DEVELOPERS](https://slackonly.com/developers.html) and [QUALITY_CONTROL](https://slackonly.com/quality_control.html)

## Contact

* Web Site: [www.slackonly.com](https://slackonly.com)
* Project Lead:  Panagiotis Nikolaou [hostmaster -at- slackonly -dot- com]()

## Copyright

* SlackwareŽ is a Registered Trademark of Patrick Volkerding.
* Linux is a Registered Trademark of Linus Torvalds.

---

[1]: https://slackbuilds.org/
[2]: https://packages.slackonly.com/pub/packages/14.1-x86/
[3]: https://packages.slackonly.com/pub/packages/14.1-x86_64/
[4]: https://packages.slackonly.com/pub/packages/14.2-x86/
[5]: https://packages.slackonly.com/pub/packages/14.2-x86_64/
