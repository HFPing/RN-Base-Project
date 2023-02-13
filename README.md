# Ract Native Base Project

Base react native project with defined architecture, appropriate documentation and example implementations

## Motivation

React native project standardization is a difficult task when stating a project from scratch, or trying to update an existing project.
This repo aims to define a standard/common structure with which RN projects can be based upon, in order to accelerate and simplify the way the project is assimilated, documentation is implemented, code elements are developed and overall architecture of it.

## Objectives

1. Create a base React Native _template_ project with which more specific projects can be created
    - This template must implement an scalable architecture to facilitate and make implementations _procedural_ (implementing new features should be part of a guideline, to make them faster at least)
    - Must implement a clear example of test suites for many different types of screens
    - The template should preferably follow a design pattern, like MVVM, to focus testing on the business logic

2. Implement scripts/procedures to make the release packages of the application to have them ready to be uploaded to stores
    - Many teams usually just stick to making the debug build on android, which is most likely not the best option for production release
    - _[Obfuscation][obfs]_ should also be researched in case the package gets decrypted, to keep the JS code secure (look for how to see the JS code on the APK package at least)

3. Implement some means/ways to easily document the application
    - As a piece of software, is important to keep documentation on the project to keep track of the general architecture, architecture changes, dependencies, screens and data flow
    - The desired outcome is to implement some kind of normalized/standard way to keep documentation files in the repo, with the possibility of _exporting them_ to be used in more formal documentation
    - The software to create/generate this documentation must be of asy access, free ad open source sounds like a good idea, like [Draw.io][drawio] (must be research further as there is a pricing in the site)
    - Although this goal focuses on _traditional documentation_, clean code that attempts to document itself should also be aimed for. One guide to try to make this possible can be the [SOLID Principles][solid]

4. Branching model
    - Although standard, a good foundation to start developing a production software is a good branching model to know what is the code running in the different environments an organization may have
    - There a re many [branching strategies][branch_strategy], but for now the [Git Flow][git_flow] will be followed

5. Integration with CI pipeline
    - Automation of certain tasks is a necessary feature for repositories
    - For now, [Github Actions][github_actions] will only be implemented

6. RN version migration procedure/strategy
    - React Native hasn't had a release version as of yet. Every new minor version introduces sometimes breaking changes that make migration from lower versions very hard
    - Some kind of strategy or tool would be helpful to aid in this version migration task

7. Environment management
    - Software projects rely on many environments that run and communicate with different systems. Separating and controlling when and which system to use every time is a necessary feature for apps
    - The most common way to handle this task is to use [.env files][env_file]

8. Release (with corresponding notes) handling
    - This point refers mostly on how manage release notes
    - When making a new release for customers/end user, it's necessary to summarize what new features/fixes are added in each new release
    - Although they could be done manual, it's desirable to handle them in an automated way

9. Remote debugging
    - A lot of times, there are issues with the app on customer/end user devices, which makes it particularly hard to assess the cause of the issue without a specific environment to replicate it
    - As such, a way or method to be able to assess the cause of issues is needed. Remote information logging, user feedback, automated tests for different scenarios, QA team?, etc

10. Metrics gathering. Analytics
    - Recording usability and data from apps can be a way to understand how the end user interacts with the app, what areas are most used, as well as gathering data that can be used in some ways
    - Probably the most straightforward library to implement is [Google Analytics][google_analytics]

11. Dependencies decoupling
    - Following the topic of SOLID principles as a base for a healthy codebase, it's important to implement [Dependency Inversion][depdendency_inversion] to be able to respond quickly to big and small changes in dependencies/"providers" for some kind of functionality
    - Although not all dependencies should be decoupled (probably) as many as possible should. Specially the ones acting as "information providers"

12. Typescript migration
13. Static and dynamic? code analysis. (Sonar, rules, unused code)
14. Adaptable to many screen sizes. Tablet and smartphone into consideration

## Developer environment

Assuming it's development in a mac OS machine

- [React native development setup][RN_Dev]
  - Won't list specific OS dependencies. They are listed and maintained in the official page

- [Node JS][NodeJS] (Version 16.16.0 used for startup)
  - React Native is a NodeJS project at it's code, so a local Javascript runtime environment is necessary
  - There are other runtime environments worth researching to use in RN, like [Bun], which is supposedly faster in many ways
  - It's recommended to use to version manager tool to handle different versions of node, as other projects (using different versions of react native or different projects altogether) like [Fast Node Manager][fnm]

- [XCode] (Version 13.4.1 used for startup) for iOS development
  - A lot of times, projects depend upon specific versions of this IDE. Downloading it from the App Store may not always make a project work, so it's advices to specify and keep the version used when the app was first created
  - Since you can only download the latest XCode version using the App Store, it's encouraged to use the [Apple Developer Download Site][Apple_Dev_Download] to download a specific version

- [Android Studio][Android_Studio] for Android development
  - Unlike XCode, this IDE doesn't seem to break builds with updates, so it's recommended to keep it, as well as it's internal dependencies, updated. Particularly the emulator

- [Java Development Kit][JDK_Info] (Version 11.0.5 used for startup) for CLI Android builds
  - This and version 8 usually works fine. Later versions haven't worked with the current version of React Native
  - As to keep and maintain specific java versions (if necessary), it's recommended to use [jEnv] to manage and install specific versions and switch between them in the machine
  - Open JDKs downloaded from Homebrew work just fine

---

## Local execution

As this is just a base template for apps, it does not contemplate environments. The app build on top of this must implement their own environment-dependant build commands. (Regardless this, the necessary libraries must be implemented in this base repository since it's common for all other apps to implement environment builds)

### 1. Install dependencies

```bash
yarn
```

Only **yarn** will work to make the use of package managers more standardized

### 2. Local development build on emulator of physical device

For Android

```bash
yarn android:run-debug
```

For iOS:

```bash
yarn ios
```

## Generate product

Following the official [documentation][build-android-release], we can create the AAB with:

```bash
cd android
./gradlew bundleRelease
```

A modified version of the command was implemented to generate APKs (mainly for internal test or release verification user tests) executing the command:

```bash
yarn android:build-release
```

It generates the APK in the path: [android/app/build/outputs/apk/release/app-release.apk](android/app/build/outputs/apk/release/)

---

## Project Structure

This project implements an opinionated structure (directory/folder structure) that tries to generalize, simplify and make it "a procedure" to know where and how to select a directory for any new files (screens, components, variables, services, etc) and existing files in order to make it easier to locate. It is encouraged to try to stick to the structure proposed here, but ultimately it has to be adapted to whatever the team requirements are.

The folder structure is the following:

>📂 android: Native Android project. Many android specific configurations go in some files in this folder. Usually it's not necessary to add any code to any file inside this folder\
📂 ios: Native iOS project. iOS specific configurations go inside this project. Can be opened in XCode by opening the workspace.\
📂 [src](src/SrcFolder.md): Source code of the application. All react native code and necessary extra files should be in this folder.

Files:

>📜 .buckconfig: **Research needed.** Not a completely necessary file for the project, but useful in using this [Buck build tool][buck].\
📜 .eslintrc.js: Lint rules file that [ESLint][eslint] takes to point issues in code syntax. It also contemplates extensions, modules and special configurations of this tool.\
📜 .flowconfig: [Flow][flow] configuration file. By no means it's a necessary file for the project since Typescript is already configured, but it's left as an alternative for static typing checker.\
📜 .gitignore: File used to enlist files, directories or expressions to exclude files from watching them in the version control system.\
📜 .npmrc: NPM configuration file. It defines the settings on how NPM should behave when running commands.\
📜 .prettierrc.js: [Prettier][prettier] configuration file.\
📜 .ruby-version: File that specifies the ruby version to be used. Useful for iOS development.\
📜 .watchmanconfig: [Watchman][watchman] configuration file. It's not completely necessary, since watchman will load the global default configuration file if it didn't exist. It's probably a good idea to keep it to have this configurations declared and known.\
📜 Gemfile: Related to the iOS project exclusively. Seems to be [necessary][gemfile], but research is needed.\
📜 app.json: Doesn't seem to be very necessary. It only takes the "app name" for the renderer in _index.js_. Could be deleted by setting this name directly in this file.\
📜 babel.config.js: [Babel][babel] configuration file.\
📜 index.js: Project root file. Must keep the _.js_ extension. This file renders the main file located in scr, so there's mostly no need to write code here.\
📜 jest.config.js: [Jest][jest] configuration file\
📜 metro.config.js: [Metro][metro] configuration file\
📜 tsconfig.json: [Typescript][typescript] configuration file

---

## General information

[Adding TypeScript to an Existing Project​](https://reactnative.dev/docs/typescript#adding-typescript-to-an-existing-project)

[Comparing statically typed JavaScript implementations. PropTypes vs. React Flow vs. TypeScript](https://blog.logrocket.com/typescript-vs-flow-vs-proptypes/)

[app.json file. What is the purpose of app.json file? Is it safe to delete it?](https://github.com/react-native-community/cli/issues/1113)

[Understanding Babel as a native developer working with React Native](https://medium.com/@flexaddicted/understanding-babel-as-a-native-developer-dived-into-react-native-8cbf632318af)

[Testing React Native Apps](https://jestjs.io/docs/27.x/tutorial-react-native)

---

[XCode]: https://developer.apple.com/xcode/
[RN_Dev]: https://reactnative.dev/docs/environment-setup
[Apple_Dev_Download]: https://developer.apple.com/download/all/
[Android_Studio]: https://developer.android.com/studio
[JDK_Info]: https://www.ibm.com/docs/en/i/7.3?topic=platform-java-development-kit
[jEnv]: https://www.jenv.be
[NodeJS]: https://nodejs.org/en/
[Bun]: https://bun.sh
[fnm]: https://github.com/Schniz/fnm
[obfs]: https://en.wikipedia.org/wiki/Obfuscation
[drawio]: https://drawio-app.com
[solid]: https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design
[branch_strategy]: https://dev.to/arbitrarybytes/comparing-git-branching-strategies-dl4
[git_flow]: https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow
[github_actions]: https://github.com/features/actions
[env_file]: https://www.ibm.com/docs/en/aix/7.2?topic=files-env-file
[google_analytics]: https://analytics.google.com/analytics/web/provision/#/provision
[depdendency_inversion]: https://stackify.com/dependency-inversion-principle/
[build-android-release]: https://reactnative.dev/docs/signed-apk-android#generating-the-release-aab
[buck]: https://github.com/facebook/buck/
[eslint]: https://eslint.org
[flow]: https://flow.org/en/
[prettier]: https://prettier.io
[watchman]: https://facebook.github.io/watchman/
[gemfile]: https://guides.cocoapods.org/using/a-gemfile.html
[babel]: https://babeljs.io
[jest]: https://jestjs.io
[metro]: https://facebook.github.io/metro/
[typescript]: https://www.typescriptlang.org
