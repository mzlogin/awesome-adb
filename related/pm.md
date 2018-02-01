# pm 相关命令


<!-- vim-markdown-toc GFM -->

* [pm --help](#pm---help)
* [查看手机中APK的存放位置](#查看手机中apk的存放位置)

<!-- vim-markdown-toc -->

## pm --help
```sh
usage: pm list packages [-f] [-d] [-e] [-s] [-3] [-i] [-u] [--user USER_ID] [FILTER]
       pm list permission-groups
       pm list permissions [-g] [-f] [-d] [-u] [GROUP]
       pm list instrumentation [-f] [TARGET-PACKAGE]
       pm list features
       pm list libraries
       pm list users
       pm path PACKAGE
       pm dump PACKAGE
       pm install [-lrtsfd] [-i PACKAGE] [--user USER_ID] [PATH]
       pm install-create [-lrtsfdp] [-i PACKAGE] [-S BYTES]
               [--install-location 0/1/2]
               [--force-uuid internal|UUID]
       pm install-write [-S BYTES] SESSION_ID SPLIT_NAME [PATH]
       pm install-commit SESSION_ID
       pm install-abandon SESSION_ID
       pm uninstall [-k] [--user USER_ID] PACKAGE
       pm set-installer PACKAGE INSTALLER
       pm move-package PACKAGE [internal|UUID]
       pm move-primary-storage [internal|UUID]
       pm clear [--user USER_ID] PACKAGE
       pm enable [--user USER_ID] PACKAGE_OR_COMPONENT
       pm disable [--user USER_ID] PACKAGE_OR_COMPONENT
       pm disable-user [--user USER_ID] PACKAGE_OR_COMPONENT
       pm disable-until-used [--user USER_ID] PACKAGE_OR_COMPONENT
       pm hide [--user USER_ID] PACKAGE_OR_COMPONENT
       pm unhide [--user USER_ID] PACKAGE_OR_COMPONENT
       pm grant [--user USER_ID] PACKAGE PERMISSION
       pm revoke [--user USER_ID] PACKAGE PERMISSION
       pm reset-permissions
       pm set-app-link [--user USER_ID] PACKAGE {always|ask|never|undefined}
       pm get-app-link [--user USER_ID] PACKAGE
       pm set-install-location [0/auto] [1/internal] [2/external]
       pm get-install-location
       pm set-permission-enforced PERMISSION [true|false]
       pm trim-caches DESIRED_FREE_SPACE [internal|UUID]
       pm create-user [--profileOf USER_ID] [--managed] USER_NAME
       pm remove-user USER_ID
       pm get-max-users

pm list packages: prints all packages, optionally only
  those whose package name contains the text in FILTER.  Options:
    -f: see their associated file.
    -d: filter to only show disbled packages.
    -e: filter to only show enabled packages.
    -s: filter to only show system packages.
    -3: filter to only show third party packages.
    -i: see the installer for the packages.
    -u: also include uninstalled packages.

pm list permission-groups: prints all known permission groups.

pm list permissions: prints all known permissions, optionally only
  those in GROUP.  Options:
    -g: organize by group.
    -f: print all information.
    -s: short summary.
    -d: only list dangerous permissions.
    -u: list only the permissions users will see.

pm list instrumentation: use to list all test packages; optionally
  supply <TARGET-PACKAGE> to list the test packages for a particular
  application.  Options:
    -f: list the .apk file for the test package.

pm list features: prints all features of the system.

pm list users: prints all users on the system.

pm path: print the path to the .apk of the given PACKAGE.

pm dump: print system state associated with the given PACKAGE.

pm install: install a single legacy package
pm install-create: create an install session
    -l: forward lock application
    -r: replace existing application
    -t: allow test packages
    -i: specify the installer package name
    -s: install application on sdcard
    -f: install application on internal flash
    -d: allow version code downgrade
    -p: partial application install
    -g: grant all runtime permissions
    -S: size in bytes of entire session

pm install-write: write a package into existing session; path may
  be '-' to read from stdin
    -S: size in bytes of package, required for stdin

pm install-commit: perform install of fully staged session
pm install-abandon: abandon session

pm set-installer: set installer package name

pm uninstall: removes a package from the system. Options:
    -k: keep the data and cache directories around after package removal.

pm clear: deletes all data associated with a package.

pm enable, disable, disable-user, disable-until-used: these commands
  change the enabled state of a given package or component (written
  as "package/class").

pm grant, revoke: these commands either grant or revoke permissions
    to apps. The permissions must be declared as used in the app's
    manifest, be runtime permissions (protection level dangerous),
    and the app targeting SDK greater than Lollipop MR1.

pm reset-permissions: revert all runtime permissions to their default state.

pm get-install-location: returns the current install location.
    0 [auto]: Let system decide the best location
    1 [internal]: Install on internal device storage
    2 [external]: Install on external media

pm set-install-location: changes the default install location.
  NOTE: this is only intended for debugging; using this can cause
  applications to break and other undersireable behavior.
    0 [auto]: Let system decide the best location
    1 [internal]: Install on internal device storage
    2 [external]: Install on external media

pm trim-caches: trim cache files to reach the given free space.

pm create-user: create a new user with the given USER_NAME,
  printing the new user identifier of the user.

pm remove-user: remove the user with the given USER_IDENTIFIER,
  deleting all data associated with that user
```

## 查看手机中APK的存放位置
```sh
adb shell pm list packages -f
```

示例：
```sh
adb shell pm list packages -f | grep vivo 

output:
package:/system/app/BBKWeatherProvider/BBKWeatherProvider.apk=com.vivo.weather.provider
package:/system/app/VivoSmartMultiWindow/VivoSmartMultiWindow.apk=com.vivo.smartmultiwindow
package:/system/app/CoffeeTime/CoffeeTime.apk=com.vivo.livewallpaper.coffeetime
package:/system/app/SetupWizard/SetupWizard.apk=com.vivo.setupwizard
...
```
