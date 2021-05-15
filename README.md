# electron-sharp-demo

Demo app to reproduce bug with packaging Sharp with Electron.

## How this repo was created

These steps were performed on Ubuntu 20.04.2, running in WSL2 on Windows 10.

1. Generated using steps from https://www.electronforge.io/templates/typescript-+-webpack-template
2. Installed `sharp` and type defs with following args (npm v6):

```
npm install sharp --build-from-source --unsafe-perm
```

3. Updated `webpack.renderer.config.js` to add sharp to `externals` fields
4. Updated `src/renderer.ts` script to call Sharp
5. Updated `src/index.ts` to set `nodeIntegration` to `true` and `contextIsolation` to `false`

## The issue

When the Electron app is packaged for distribution, Sharp is not bundled with it.

### Working - running in Dev using `electron-forge start`

From the application root, run:

```
npm start
```

The basic Electron Forge demo window will open. The console should contain no errors, and show the `sharp` object definition being printed out.

### Not working - packaging application and executing

From the application root, run:

```
npm run package
```

Once completed, run the generated executable. E.g. on Linux:

```
out/electron-sharp-demo-linux-x64/electron-sharp-demo
```

The basic Electron Forge demo window will open. This time, the console will contain the following error:

```
Uncaught Error: Cannot find module 'sharp'
```
