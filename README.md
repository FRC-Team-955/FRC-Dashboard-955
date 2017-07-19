# FRC-Dashboard-955

Dashboard for viewing robot data and configuration while running built on electron. Special thanks to [FRCDashboard](https://github.com/FRCDashboard) and [pynetworktables2js](https://github.com/robotpy/pynetworktables2js) for creating the tools and starting point for this project.

## Setup
### Dependencies

* Python 3 **(MUST be 3, not 2!)**
* `pynetworktables2js`

        py -m pip install pynetworktables2js

If you're going to be using the preferred method of using the dashboard (as an application), you'll also need:
* [`nodejs`](https://nodejs.com) & [`npm`](https://npmjs.com)
* Electron (to install, `cd` into dashboard directory and run `npm install`)

### Configuration

* In `ui.js`, there's a large `switch` statement in the `onValueChanged()` function which controls the updating of control elements in the dashboard. Example NetworkTables key names are used, but you'll need to change them to match those used in your team's robot code for them to affect anything on your robot.

* You also need to set up the address of the network tables server you are connecting to, which is usually the robot. In the `main.js` file, change the address from `localhost` after the `--robot` argument when starting the python server to the address you want to use. It will usually be `roborio-XXXX-frc.local` where XXXX is you're team number, such as `roborio-955-frc.local`

### Testing

If you want to test, but don't have access to a robot, then you can use the Outline Viewer to run a network table server as if it were the robot. It can be found at `C:\Users\$NAME\wpilib\tools\OutlineViewer.jar`. Just run it and select server, then you can connect to it from the dashboard at the address `localhost`.

### Using dashboard as Application

The preferred method of using the dashboard is to run it using the [Electron](http://electron.atom.io) framework. Your dashboard will be its own application, and will be easy to manipulate.

While in the dashboard directory, run:

    npm start

This will start a Python server and open the dashboard application. Note that you don't have to close and reopen the application every time you make a change, you can just press `Ctrl+R` (`Cmd+R` on Mac) to refresh the application.

### Making a release

To package your app into an installer use command:

```
npm run release
```

It will start the packaging process and ready for distribution file will be outputted to `dist` directory.

All packaging actions are handled by [electron-builder](https://github.com/electron-userland/electron-builder). It has a lot of [customization options](https://github.com/electron-userland/electron-builder/wiki/Options), which you can declare under ["build" key in package.json file](https://github.com/szwacz/electron-boilerplate/blob/master/package.json#L2).

If you want to package your app for multiple operating systems from your own machine [electron-builder kind of supports this](https://github.com/electron-userland/electron-builder/wiki/Multi-Platform-Build), but there is a lot of asterisks. That's why this boilerplate is configured so only package for the OS you're running on is created (you can of course change it).