# MacOS Finder Custom Directory Right Click Menu

## Fork changes (@mchampanis)

- update `README.md` to properly reflect project settings and description
- prevent default scripts being recreated repeatedly if you've already set app up
- prevent multiple copies of app running
- macOS Sonoma build with the above released

## Description

This application allows you to add custom right click menu items to directories opened in MacOS Finder.
Right click menu items can be added as shell scripts.
The application comes with two script files inbuilt to create new text documents in the current directory and to open terminal from the current directory.
The application has been tested to work up to macOS Tahoe `26.2`.

## Download the Application

[Download macOS Sonoma binary](https://github.com/mchampanis/custom-finder-right-click-menu/releases).

You can download a pre-built app file that is ready to run from the above link.

You can build the application from the source code on macOS using Xcode.

## Building

- Open `FinderMenu.xcodeproj` with Xcode
- Set target to `FinderMenu`
- `Product` > `Archive` to build the release version
- Follow instructions and click the `Distribute` button at some point to save `FinderMenu.app` somewhere useful

## Using the Application

Using the application is very simple.
Copy `FinderMenu.app` to your `/Applications` directory.
Run `FinderMenu.app` once from the `/Applications` directory in your system to setup right click menu items.

When you run `FinderMenu.app` once, the application will take the following steps to setup the right click menu items.

* Install a launch agent to serve the custom right click menu items.
* Install a Finder extension to include custom right click menu items in the Finder.
* Creates `~/.config/findermenu` directory to place custom right click menu scripts.
* Enable `FinderMenuItems` in `System Preferences > Extensions > Finder Extensions` in case it is not already enabled.

Right click menu service in `FinderMenu.app` automatically starts with your system.
Because of that you do not have to run `FinderMenu.app` ever again unless you do not want to make changes to the menu item scripts.
However, `FinderMenu.app` should always be present in your `/Applications` directory for the menus to work.

Following gif shows how the provided `New Text File Here` menu item works.

![alt text](Media/finder-right-click-new-text.gif "New text File Here")

The next gif shows how the provided `Open Terminal Here` menu item works.

![alt text](Media/finder-right-click-open-terminal.gif "Open Terminal Here")

## Adding Custom Menu Items

Adding a new right click menu item is as simple as creating a shell script in the `~/.config/findermenu` directory.
The shell script should accept the path to the directory as the first argument when running the script.
File name of the script file becomes the menu item name in the right click menu.
When the menu item is clicked, the script is executed with the directory path as the first argument.
You can refer to the given scripts in `~/.config/findermenu` for examples.
When you place a new script in `~/.config/findermenu`, reload FinderMenu to refresh settings:

```zsh
launchctl kickstart -k gui/501/com.samiyuru.findermenuservice
```

## Reset to default scripts

Remove the `~/.config/findermenu` directory and restart FinderMenu:

```zsh
launchctl kickstart -k gui/501/com.samiyuru.findermenuservice
```

## Uninstall the Application

You can take the following steps if you need to completely uninstall the application form your system.

* Delete the `FinderMenu.app` from `/Applications` directory.
* Delete the `~/.config/findermenu` directory.
* Disable the finder extension by going to `System Preferences > Extensions > All` and disabling the FinderMenu item.
* Remove the launch agent by deleting `\~/Library/LaunchAgents/com.samiyuru.findermenuservice.plist`


## Credits

The icon used in the application is a modified version of an icon made by [Freepik](https://www.flaticon.com/authors/freepik) from [www.flaticon.com](https://www.flaticon.com).
