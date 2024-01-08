## Revert New Discord Layout

How to use this script:
1. Go to https://discord.com/app
2. Press `Ctrl + Shift + I` to open DevTools
3. Go to the `Console` tab
4. Paste the following code and hit enter:

```js
let wpRequire;
window.webpackChunkdiscord_app.push([[ Math.random() ], {}, (req) => { wpRequire = req; }]);

let UserSettingsActions = Object.values(wpRequire.c).find(x => x?.exports?.PreloadedUserSettingsActionCreators).exports;
let ProtobufTypes = Object.values(wpRequire.c).find(x => x?.exports?.BoolValue).exports;

UserSettingsActions.PreloadedUserSettingsActionCreators.updateAsync("appearance", data => {
    data.mobileRedesignDisabled = ProtobufTypes.BoolValue.create({value: true})
}, UserSettingsActions.UserSettingsDelay.INFREQUENT_USER_ACTION)
```

This code requires no changes, preserves all your other appearance settings (such as theme), as well as automatically includes all relevant Discord headers, reducing any risks to minimum.

### How does this work?
This emulates flipping the `Show New Layout` toggle in appearance settings. Yes the toggle is server-synced for some reason.

Note: This is only a temporary solution. Discord will start ignoring that setting in some future update.
___
This was inspired by [@xeuk](https://gist.github.com/Xeukxz/a1b55f38f5ede22e757b3894430066db/c387c85e729e62b37b36d8eb0ea1d5b3dde0b1a8)'s original snippet
