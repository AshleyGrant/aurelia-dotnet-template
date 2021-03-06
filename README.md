
<div align="center">
    <a href="https://aurelia.io/">
        <img width="150" height="150" src="https://cdn.worldvectorlogo.com/logos/aurelia-1.svg">
    </a>
    <a href="https://webpack.js.org/">
        <img width="150" height="150" hspace="10" src="https://cdn.rawgit.com/webpack/media/e7485eb2/logo/icon-square-big.svg">
    </a>
    <a href="https://github.com/Microsoft/TypeScript">
        <img width="150" height="150" hspace="10" src="https://cdn.worldvectorlogo.com/logos/typescript.svg">
    </a>
    <a href="https://www.microsoft.com/net/download/windows">
        <img width="150" height="150" hspace="15" src="https://docs.microsoft.com/en-us/dotnet/images/hub/netcore.svg">
    </a>
    <h1>aurelia-dotnet-template</h1>
</div>

### Description
This template is the result of combining what I liked from the original [JavascriptServices](https://github.com/aspnet/JavaScriptServices), MaximBalaganskiy's [AureliaDotnetTemplate](https://github.com/MaximBalaganskiy/AureliaDotnetTemplate) and the folder structure found in the code generated from the [Aurelia CLI](https://github.com/aurelia/cli).

### About
This repo uses the Aurelia framework, TypeScript, .NET Core 2, Bootstrap 4 and the latest Webpack. It has unit testing using mocha, chai and sinon as well as the e2e testing suite [testcafe](https://github.com/DevExpress/testcafe) with very basic examples included.

This repo uses font-awesome 5 instead of glyphicons. More about font-awesome 5 below.

### Prerequisites
To run this repository without issue there are a couple of tools you should have installed. If you are missing any of the below, follow the instructions and install them for your platform.
1. [.NET Core SDK (v2.0+)](https://www.microsoft.com/net/download)
2. [Yarn](https://yarnpkg.com/en/docs/getting-started)
3. [NodeJS](https://nodejs.org/en/)

### Purpose
I wanted a public location for an up to date aurelia-typescript-net-core template repository that would be easy to start new applications from. A repository with folders structured in a way that immediately makes sense, hopefully. 

And although there are excellent webpack examples in jods4's [aurelia-webpack-build](https://github.com/jods4/aurelia-webpack-build/tree/master/demos) repository, I wanted a location for a config that I know works for most of my own use-cases.

### Running the application
After pulling down the repository, navigate to the application root folder and run the following commands in your favourite CLI:

1. `dotnet restore`
2. Then select either
    1. `yarn install` or
    2. `npm install`, although yarn is assumed in prerequisites.
3. `dotnet run`

and navigate to http://localhost:5000.

To change the configured port from 5000 edit the file `Program.cs` in the root folder on the line: `.UseUrls("http://localhost:5000/")`.

### Hot module reload

In order for hot-module-reload to work you need to make sure your environment is set to development **before** running the application, for example running one of the following commands for your platform: 

1. Windows
    1. `$Env:ASPNETCORE_ENVIRONMENT = "Development"`
    2. `set ASPNETCORE_ENVIRONMENT=Development`
2. Unix
    1. `export ASPNETCORE_ENVIRONMENT=Development`

### Testing
There are two npm scripts saved to the `package.json`. 

##### Unit
Running `npm run test` runs the unit tests located in `test/unit/*.spec.ts`.

##### E2E
First run the application and then from a new CLI run `npm run testcafe`, this will run the e2e tests located in `test/e2e/*`.

It's configured to use firefox, if you wish to use something else, for example chrome, simply change `firefox` to `chrome` under scripts in the `package.json`.

### Font-Awesome 5
I've pre-configured font-awesome 5 to use the new SVG-based framework in this repository. Since it's quite different from just importing the web-fonts css, I thought I'd describe the setup briefly.

I've added the following packages:

```js
"@fortawesome/fontawesome" // the "factory" that builds your icons
"@fortawesome/fontawesome-free-brands" // all available free icons
"@fortawesome/fontawesome-free-regular"
"@fortawesome/fontawesome-free-solid"
```

The imports can be found in `src/components/app.ts`:

```ts
import fontawesome from '@fortawesome/fontawesome';
import { faHome, faPlus, faThList } from '@fortawesome/fontawesome-free-solid';

// Pre-registering icon definitions so that you do not have to explicitly pass them to render an icon.
fontawesome.library.add(faHome, faPlus, faThList /*solid, etc..*/);
...
    config.map([{
        ...
        settings: { 
                icon: faHome.iconName, // the name of the imported icon
                prefix: faHome.prefix // the icon prefix, fas/far/fab etc.
            },
        ...
    },
...
```

The router settings defined in app.ts are used in the navmenu (`src/components/navmenu/navmenu.html`):
```html
...
<a...>
    <span class="${row.settings.prefix} fa-${row.settings.icon}"></span> ${row.title}
</a>
...
```

If you want to add an icon that can be used later without explicit imports, simply append it to the end of `fontawesome.library.add(faCameraRetro, ...` defined above. You could then in other files just use the icon name directly like you might be used to: 

```html
<i class="fas fa-camera-retro"></i>
```