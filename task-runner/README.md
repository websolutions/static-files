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