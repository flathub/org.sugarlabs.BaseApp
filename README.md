# Sugar Labs BaseApp

This BaseApp contains dependencies shared between ALL Sugar Labs applications.

## How To Build

```
git clone --recurse-submodules https://github.com/flathub/org.sugarlabs.BaseApp.git
cd org.sugarlabs.BaseApp
flatpak --user remote-add --if-not-exists flathub-beta https://flathub.org/beta-repo/flathub-beta.flatpakrepo
flatpak --user install flathub-beta org.gnome.{Platform,Sdk}//46beta
flatpak-builder --user --force-clean --install build org.sugarlabs.BaseApp.json
```

## How To Update

```
cd org.sugarlabs.BaseApp
git submodule update --remote
flatpak --user install org.flathub.flatpak-external-data-checker
```

Then edit `org.sugarlabs.BaseApp.json` to:

1. Bump GNOME runtime to the latest stable version, e.g. `"runtime-version": "46beta"`
2. Bump Python version references to the one included in the GNOME runtime, e.g. `flatpak --user run --command=python org.gnome.Platform//46beta --version`
3. Bump Perl version references to the one included in the GNOME SDK, e.g. `flatpak --user run --command=perl org.gnome.Sdk//46beta --version`
4. Update `shared-modules` submodule with `git submodule update --remote`.
5. Update every single module to the latest stable version. e.g. use `flatpak run --filesystem=$PWD org.flathub.flatpak-external-data-checker org.sugarlabs.BaseApp.json`

## How To Add New Modules

1. Search on flathub's github for an existing example, e.g. `org:flathub dbus-python-1.3.2`.
2. For Python modules use [flatpak-pip-generator](https://github.com/flatpak/flatpak-builder-tools).
3. For tarballs or git modules use [anitya](https://release-monitoring.org/) long with [flatpak-external-data-checker](https://github.com/flathub/flatpak-external-data-checker).