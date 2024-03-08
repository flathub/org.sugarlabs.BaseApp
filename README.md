# Sugar Labs BaseApp

This BaseApp contains dependencies shared between ALL Sugar Labs applications.

### Important  Note
If you have installed GNOME runtime/Sdk system-wide than omit `--user` from each command  
example:

~`flatpak --user run --command=python org.gnome.Platform//45 --version`~  
`flatpak run --command=python org.gnome.Platform//45 --version`

## How To Build

```
git clone --recurse-submodules https://github.com/flathub/org.sugarlabs.BaseApp.git
cd org.sugarlabs.BaseApp
flatpak -y --user install org.gnome.{Platform,Sdk}//45
flatpak-builder --user --force-clean --install build org.sugarlabs.BaseApp.json
```

## How To Update

```
cd org.sugarlabs.BaseApp
git submodule update --remote
flatpak --user install org.flathub.flatpak-external-data-checker
```

Then edit `org.sugarlabs.BaseApp.json` to:


1. Bump GNOME runtime to the latest stable version, e.g. `"runtime-version": "45"`
2. Bump Python version references to the one included in the GNOME runtime, e.g. `flatpak --user run --command=python org.gnome.Platform//45 --version`
3. Bump Perl version references to the one included in the GNOME SDK, e.g. `flatpak --user run --command=perl org.gnome.Sdk//45 --version`
4. Update `shared-modules` submodule with `git submodule update --remote`.
5. Update every single module to the latest stable version. e.g. use `flatpak run --filesystem=$PWD org.flathub.flatpak-external-data-checker org.sugarlabs.BaseApp.json`

## How To Add New Modules

1. Search on flathub's github for an existing example, e.g. `org:flathub dbus-python-1.3.2`.
2. For Python modules use [flatpak-pip-generator](https://github.com/flatpak/flatpak-builder-tools).
3. For tarballs or git modules use [anitya](https://release-monitoring.org/) long with [flatpak-external-data-checker](https://github.com/flathub/flatpak-external-data-checker).
