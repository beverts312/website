---
date: 2018-03-05
title: "Visual Studio Code Tips and Tricks"
author: Bailey Everts
---

[Visual Studio Code](https://code.visualstudio.com/) is a powerful and extensible IDE. It is the only IDE I use, here are a few tips to help optimize your VS Code experience.

### Debugging
One of the best things about VS Code is that with the help of a few extensions it can debug almost any language. Debugging is configured through the .vscode/launch.json. Below are some examples of what it takes to debug different languages in VS Code.

#### C Sharp
* [launch.json](https://github.com/beverts312/dev-env/blob/master/vscode/debugging/dotnet.json)
* Required Extension: [ms-vscode.csharp](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)

#### Java
Java debugging (and support) is provided through a combination of Red Hat and Microsoft extensions.
VS Code needs to use Java 8 for debugging and intelisense to work, this doesnt mean that the project needs to be Java 8, just VS code needs to be configured to use Java 8.
The provided launch.json assumes the debugger is listening on localhost:5005, this can be updated by modifying the hostName and port properties of the debug configuration.
For tests, the provided launch.json assumes localhost:5555, to expose this port during a test run appened these args to your run tests command `-Dmaven.surefire.debug="-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=5555 -Xnoagent -Djava.compiler=NONE"`.

* [launch.json](https://github.com/beverts312/dev-env/blob/master/vscode/debugging/java.json)
* Required Extension: [vscjava.vscode-java-pack](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)

#### Go
* [launch.json](https://github.com/beverts312/dev-env/blob/master/vscode/debugging/go.json)
* Required Extension: [lukehoban.go](https://marketplace.visualstudio.com/items?itemName=golang.Go)

#### Node
Node debugging is supported natively by VS Code.

* [Current file Launch.json](https://github.com/beverts312/dev-env/blob/master/vscode/debugging/node-current.json)
* [App with entrypoint file Launch.json](https://github.com/beverts312/dev-env/blob/master/vscode/debugging/node-entrypoint.json)

#### Web Apps
Modern web apps require different debug configurations depending on how the source is transpiled (or if it even is transpiled).

The key value to configure when trying to debug a web app is webRoot key. This directory should contain the main entry point to the web app.

~The jest plugin claims to support debugging but I have yet to get that aspect of the extension to work (still an awesome extension tho). If that works for you great, if not you can just use the node debugger that comes with vscode by default.~

For webpack debugging it is important that your webpack config includes:
```
    devtool: 'source-map',
    output: {
        publicPath: '/',
        ...
    },
    ...
```

* Required Extension for Chrome: [msjsdiag.debugger-for-chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)
* Required Extension for Firefox: [hbenl.vscode-firefox-debug](https://marketplace.visualstudio.com/items?itemName=firefox-devtools.vscode-firefox-debug)
* [Generic web app Launch.json](https://github.com/beverts312/dev-env/blob/master/vscode/debugging/web.json)
* [Webpack compiled Launch.json](https://github.com/beverts312/dev-env/blob/master/vscode/debugging/webpack.json)
* [Jest Launch.json](https://github.com/beverts312/dev-env/blob/master/vscode/debugging/jest.json)

### Extensions
A lot of Visual Studio Code's power comes from it's extensability. The community is extremely active and new extensions are available on the [marketplace](https://marketplace.visualstudio.com/vscode) every day.

You can add reccomended extensions to a project by adding a `.vscode/extensions.json` file to it.

Below are a few recommended extensions.

#### Language Support
* [C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)
* [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)
* [Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)
* [Markdown](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)
* [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
* [Go](https://marketplace.visualstudio.com/items?itemName=golang.Go)

#### Miscellaneous
* [Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner) - This extension allows you to execute the opened file (supports a variety of languages).
* [Editor Config](https://marketplace.visualstudio.com/items?itemName=EditorConfig.editorconfig) - Provides editorconfig support
* [Status Bar Tasks](https://marketplace.visualstudio.com/items?itemName=GuardRex.status-bar-tasks) - This extension allows tasks defined in tasks.json to become buttons on the bottom bar of your IDE. This extensions is badass
* [TODO Highlighter](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight) - Highlightes TODO's in comments
* [Live Share](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare) - Tool for collaborative coding

#### Git
* [Git Lens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) - Provides a bunch of awesome git features. This extensions is badass
* [Git History](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory) - Provides a good visualizer for git history

#### Icons / Themes
* [Linux Themes](https://marketplace.visualstudio.com/items?itemName=SolarLiner.linux-themes) - I am a huge fan of the Monokai Dimmed theme provided by this extension
* [Icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons)
* [Great Icons](https://marketplace.visualstudio.com/items?itemName=emmanuelbeziat.vscode-great-icons)

#### Javascript / Typescript
* [Chrome Debugger](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) - Support for debugging in chrome
* [Document This](https://marketplace.visualstudio.com/items?itemName=joelday.docthis) - Helps generated JSDocs
* [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) - ESLint highlighting and autofixing
* [Import Cost](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost) - Shows the size of imports inline
* [Jest](https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest) - Provides Jest Support. This extensions is badass
* [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense) - Provides path intelisense on imports
* [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint) - TSLint highlighting and autofixing

#### Snippets
* [thekalinga.bootstrap4-vscode](https://marketplace.visualstudio.com/items?itemName=thekalinga.bootstrap4-vscode) - Font Awesome
* [johnpapa.Angular2](https://marketplace.visualstudio.com/items?itemName=johnpapa.Angular2) - Angular (2+)

### Keyboard Shortcuts
* [Linux](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf)
* [Mac](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)
* [Windows](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)

### Settings
User Settings are configured by modifying the `settings.json` for your workspace or your machine. You can view/edit both by hitting `cmd + ` ` from within vs code.

You can find an example `settings.json` [here](https://github.com/beverts312/dev-env/blob/master/vscode/settings.json)

#### Monospaced Programming Fonts with Ligatures
Monospaced programming fonts and ligatures are both supported by Visual Studio code and make reading code easier.

Note: To use ligatures you must use a font that supports them.

A good font that supports monospacing and ligatures is [monoid](https://github.com/larsenwork/monoid). To use monoid in vscode with ligatures, first download and install it from [here](https://github.com/larsenwork/monoid). Then add these 2 properties to your `settings.json`:

```
"editor.fontLigatures": true,
"editor.fontFamily": "Monoid"
```

To read about other fonts that support ligatures and monospacing checkout Scott Hanslemen's write up [here](https://www.hanselman.com/blog/MonospacedProgrammingFontsWithLigatures.aspx).

### Snippets
A snippet is when you type an alias that represents something and then hit enter to expand it, for example in vscode by default you can type while hit enter, and then it will expand to say:
```
while (condition) {

}
```
in your file, eliminating you having to type a few things. In this case it only buys you 4 characters and a new line, but snippets can provide alot larger chunks of code than that.

You can read more about how to create your own snippets [here](https://code.visualstudio.com/docs/editor/userdefinedsnippets).