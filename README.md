# Renaming a React Native project
Describes the steps needed to rename a React Native project.  Pull requests welcome!

# Steps

## 1. Ensure you have a clean repository.

Check in any outstanding changes - you'll want to start with a clean slate.

## 2. Delete all build directories

`rimraf android/app/build android/build ios/build`

## 3. Delete all directories named with the old project name

This includes `ios/oldProjectName*` and `android/app/src/main/java/com/oldProjectName`.  The upgrade will create new directories with the new project name.

## 4. Rename the project at the top of package.json

    {
      "name": "newProjectName",

Note that **[You can't use kebob-case]**(https://github.com/facebook/react-native/issues/213).  Make it camelCase.

## 5. Run `react-native upgrade`

Overwrite all files as requested.  If you have customizations in your project, you'll go back and fix them.

## 6. Update AppRegistry.registerComponent

In your main app file (e.g. App.tsx):

`AppRegistry.registerComponent("newProjectName", () => App);`

While you're at it, check that you like your main `Component` name:

    export default class MyNewShinyApp extends Component<any, any> {

## 7. Run `react-native link`

Additionally, do this also for any native projects you have, e.g. `react-native link react-native-codepush` and `react-native-link react-native-auth0`.

## 8. Bring forward any customizations in your info.plist file

Particularly:

    <key>CFBundleDisplayName</key>
    <string>New Friendly App Name</string>

Also including any other customizations you may have, like `UIBackgroundModes`.

## 9. Update app name for Android in strings.xml

    <string name="app_name">New Friendly App Name</string>

## 10. Rename target on first line of Podfile

    target 'newProjectName' do

## 11. Search any remaining instances

Search `./ios/' and './android' for any remaining instances of the old project name.  [This article](http://blog.tylerbuchea.com/renaming-a-react-native-project/) suggests these four files in particular:

    android/settings.gradle  
    android/app/build.gradle  
    android/app/src/main/AndroidManifest.xml  
    android/app/src/main/res/values/strings.xml

## 12. Additional steps

- Restart RN packager
- Rename git repository (our local repository automatically picked up the change)
- Rename local directory and update links/shortcuts/aliases

## 13. Notes

- You may want to clear cached references: "open Xcode, hold down the Option key and from the system toolbar choose Product > Clean Build Folder" ([source](http://blog.tylerbuchea.com/renaming-a-react-native-project/))
- The `react-native-rename` project has been mentioned on Stackoverflow, though we haven't used it.
- Here's an article for [renaming apps created with Expo](https://medium.com/the-react-native-log/how-to-rename-a-react-native-app-dafd92161c35).

---

Sponsored by [2 Minute Revolution](https://2minute.fit).
