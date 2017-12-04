# Seahorse Nautilus extension
The Seahorse Nautilus extension is an extension for
[Nautilus](https://wiki.gnome.org/Apps/Nautilus) (also known as Files) which
allows encryption and decryption of OpenPGP files using GnuPG.

## Building
You can build and install the Seahorse Nautilus extension using
[Meson](http://mesonbuild.com/):
```sh
meson build
ninja -C build
ninja -C build install
```

## Issue tracker
Seahorse-Nautilus uses the GNOME Bugzilla, where you can check the
[list of open bugs](https://bugzilla.gnome.org/browse.cgi?product=seahorse) of
Seahorse with the "Nautilus" component.

If you'd like to report a bug in Seahorse-Nautilus or request an enhancement,
please file an issue using the
[appropriate form](https://bugzilla.gnome.org/enter_bug.cgi?product=seahorse&component=Nautilus).

In case of a bug, please also add reproducible steps and your version of the
Seahorse Nautilus extension.

## Contributing
If you would like to contribute a patch, you should send it in to the GNOME
Bugzilla as well. If the patch fixes an existing bug, add the patch as an
attachment to that bug report; otherwise, enter a new bug report that describes
the patch, and attach the patch to that bug report.

For more information on the recommended workflow, please read
[this wiki page](https://wiki.gnome.org/Git/WorkingWithPatches).

## More information
Seahorse and its derivatives (such as the Seahorse Nautilus extension) has its
own web page on https://wiki.gnome.org/Apps/Seahorse.

To discuss issues with developers and other users, you can subscribe to the
[Seahorse mailing list](https://mail.gnome.org/mailman/listinfo/seahorse-list)
or join [#seahorse](irc://irc.gnome.org/seahorse) on irc.gnome.org.

## License
The Seahorse Nautilus extension is released under the GPL. See COPYING for more
info.
