# Using Gulp to build CSS and JS in Visual Studio
At WSOL, CSS and JavaScript is combined and minified using Gulp. These generated files are not tracked in the Git repositories, so in order to work locally developers must generate these files as needed from the raw source files that are tracked in version control. This process is outlined below.

1. Open the project in Visual Studio.
1. Open the Task Runner Explorer Window
	* Select View -> Other Windows -> Task Runner Explorer
	![VS Image](https://raw.githubusercontent.com/websolutions/static-files/master/task-runner/task-runner-view-window.png)
1. The window will now be available in the bottom toolbar. ![VS Bottom Toolbar](https://raw.githubusercontent.com/websolutions/static-files/master/task-runner/task-runner-window.png)
1. Double-click the default task to create local CSS and JS files to use the site locally. ![Default Task Finished](https://raw.githubusercontent.com/websolutions/static-files/master/task-runner/task-runner-window-default-finished.png)
1. If task runs successfully, the exit code will be 0. If the task doesn't complete successfully please let someone know in the frontend-tools Slack channel.
1. Run the site locally using Control + F5 or just F5 (for debugging).

## Config Files
The config file for CSS and JavaScript source files is named **gulpconfig.json** and typically exists in the site root of the project. This file controls how bundles, variables, and images are handled in the default task. Below is an example of this file.

```js
{
    "bundles": [
        {
            "filename": "styles.css",
            "resources": [
                "./node_modules/normalize.css/normalize.css",
                "./node_modules/jquery.scrollbar/jquery.scrollbar.css",
                "./node_modules/slick-carousel/slick/slick.css",
                "./node_modules/@fancyapps/fancybox/dist/jquery.fancybox.css",
                "./node_modules/@cmyee/pushy/css/pushy.css",
                "./wsol/design/hi-fi/core/compiled/temp/main.css"
            ]
        },
        {
            "filename": "scripts.js",
            "resources": [
                "./node_modules/jquery/dist/jquery.js",
                "./wsol/design/hi-fi/core/js/plugins/lodash.custom.js",
                "./node_modules/enquire.js/dist/enquire.js",
                "./node_modules/jquery.scrollbar/jquery.scrollbar.js",
                "./node_modules/imagesloaded/imagesloaded.pkgd.js",
                "./node_modules/smartmenus/dist/jquery.smartmenus.js",
                "./node_modules/smartmenus/dist/addons/keyboard/jquery.smartmenus.keyboard.js",
                "./node_modules/wsol.accordion/js/wsol.accordion.js",
                "./node_modules/slick-carousel/slick/slick.js",
                "./node_modules/@fancyapps/fancybox/dist/jquery.fancybox.js",
                "./node_modules/waypoints/lib/jquery.waypoints.js",
                "./node_modules/waypoints/lib/shortcuts/sticky.js",
                "./node_modules/waypoints/lib/shortcuts/inview.js",
                "./node_modules/masonry-layout/dist/masonry.pkgd.js",
                "./node_modules/@cmyee/pushy/js/pushy.js",
                "./wsol/design/hi-fi/core/js/plugins/jq-sticky-anything.js",
                "./wsol/design/hi-fi/core/js/plugins/fluidvids.js",
                "./wsol/design/hi-fi/core/js/script.js"
            ]
        },
        {
            "filename": "scripts.head.js",
            "resources": [
                "./wsol/design/hi-fi/core/js/vendor/modernizr.js"
            ]
        }
    ],
    "directories": {
        "release": "./wsol/design/hi-fi/core/compiled/",
        "temp": "./wsol/design/hi-fi/core/compiled/temp/",
        "documentation": "./wsol/design/hi-fi/wsol/design/hi-fi/reference/",
        "cleanCss": [ "./wsol/design/hi-fi/core/compiled/**/*.css" ],
        "cleanJs": [ "./wsol/design/hi-fi/core/compiled/**/*.js" ],
        "watch": [
            {
                "src": [ "wsol/design/hi-fi/core/js/**/*.js" ],
                "tasks": [ "build:js" ]
            },
            {
                "src": [ "wsol/design/hi-fi/core/img/**/*.svg" ],
                "tasks": [ "svg:sprite", "styleguide:icons" ]
            }
        ]
    },
    "sass": {
        "filename": "main.css",
        "basePath": "wsol/design/hi-fi/core/scss/",
        //"includePaths": [
        //  "bower_components"
        //],
        "main": "main.scss"
    },
    "proxySettings": {
        "localUrl": "http://local.kiepi.wsoldev.com",
        "startPath": "/!/wsol/design/hi-fi/"
    },
    "svgSprite": {
        "svgFiles": "./wsol/design/hi-fi/core/img/**/*.svg",
        "injectIn": "./wsol/design/hi-fi/root.cshtml"
    },
    "styleguideIcons": {
        "iconPath": "./wsol/design/hi-fi/core/img/ui/icons/**/*.svg",
        "injectIn": "./wsol/design/hi-fi/reference/styleguide/index.cshtml",
        "styleguideRoot": "./wsol/design/hi-fi/reference/styleguide/root.cshtml"
    }
}
```

## Watch Task
The watch task is used to update the compiled files generated in the default task as the source files change. This task is mainly enabled by designers as they work locally.