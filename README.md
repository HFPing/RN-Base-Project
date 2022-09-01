# Ract Native Base Project
Base react native project with defined arquitecture, appropiate documentation and example implementations

# Motivation
React native project standardization is a difficult task when stating a project from sratch, or trying to update an existing project.
This repo aims to define a standar/common strucutre with wich RN projects can be based upon, in order to accelerate and simplify the way the project is assimilated, documentation is implemented, code elements are developed and overall archutecture of it.

# Objectives
1. Create a base React Native _template_ project with which more specific projects can be created
    - This template must implement an scalable arquitecture to facilitate and make implementations _procedural_ (implementing new features should be part of a guideline, to make them faster at least)
    - Must implement a clear example of test suites for many differet types of screens
    - The template should preferably follow a design pattern, like MVVM, to focus testing on the business logic

2. Implement scripts/procedures to make the release packages of the application to have them ready to be uploaded to stores
    - Many teams usually just stick to making the debug build on android, which is most likely not the best option for production release
    - _[Obfuscation][obfs]_ should also be reasearched in case the package gets decripted, to keep the JS code secure (look for how to see the JS code on the APK package at least)

3. Implement some means/ways to easily document the application
    - As a piece of software, is important to keep documentation on the project to keep track of the general architecture, architecture changes, depdencies, screens and data flow
    - The desired outcome is to implement some kind of normalized/standard way to keep documentation files in the repo, with the possibility of _exporting them_ to be used in more formal documentation
    - The sofware to create/generate this documentation must be of asy access, free ad open source sounds like a good idea, like [Draw.io][drawio] (must be research further as there is a pricing in the site)
    - Althou this goal focuses on _traditional documentation_, clean code that attempts to document itself should also be aimed for. One guide to try to make this possible can be the [SOLID Principles][solid]

4. Branching model
    - Although standard, a good foundation to start developing a production software is a good branching model to know what is the code running in the different environments an organization may have
    - There a re many [branching startegies][branch_strategy], but for now the [Git Flow][git_flow] will be followed

5. Integration with CI pipeline
    - Automation of certain tasks is a necesary feature for repositries
    - For now, [Github Actions][github_actions] will only be implemented

6. RN version migration procedure/strategy
    - React Native hasn't had a release version as of yet. Every new minor version introduces sometimes breaking changes that make migration from lower versions very hard
    - Some kind of strategy or tool would be helpful to aid in this version migration task

7. Environment management
    - Software projects rely on many enviroments that run and comunicate with different systems. Separating and controling when and which system to use everytime is a necessary feature for apps
    - The most common way to handle this task is to use [.env files][env_file]

8. Release (with corresponding notes) handling
    - This point refers mostly on how manage release notes
    - When making a new release for customers/end user, it's necessary to sumarize what new features/fixes are added in each new release
    - Although they could be done manual, it's desirable to handle them in an automated way

9. Remote debugging
    - A lot of times, there are issues with the app on customer/end user devices, which makes it particulary hard to assess the cause of the issue withouth a specific environment to replicate it
    - As such, a way or method to be able to assess the cause of issues is needed. Remote information logging, user feedback, automated tests for different scenarios, QA team?, etc

10. Metrics gathering. Analytics
    - Recording usability and data from apps can be a way to understand how the end user interacts with the app, what areas are most used, as well as gathering data that can be used in some ways
    - Probably the most straightforward library to implament is [Google Analytics][google_analytics]

11. Dependencies decoupling
    - Folloing the topic of SOLID principles as a base for a healthy codebase, it's important to implement [Dependency Inversion][depdendency_inversion] to be ablo to respond quickly to big and small changes in dependencies/"proiders" for some kind of functionality
    - Althought not all dependencies should be decoupled (probably) as many as possible should. Specially the ones acting as "information providers"

12. Typescript migration
13. Static and dynamic? code analysis. (Sonar, rules, unused code)
14. Adaptable to many screen sizes. Tablet and smartphone into consideration


# Developer environment
Assuming it's development in a mac OS machine

- [React native development setup][RN_Dev]
    - Won't list specific OS dependencies. They are listed and maintained in the official page

- [Node JS][NodeJS] (Version 16.16.0 used for startup)
    - React Native is a NodeJS project at it's code, so a local Javascript runtime enviroment is necessary
    - There are other runtime environments worth researching to use in RN, like [Bun], which is supposedly faster in many ways
    - It's recommendede to use to version manager tool to handle different versions of node, as other projects (using different versions of react native or different projects alltogether) like [Fast Node Manager][fnm]

- [XCode] (Version 13.4.1 used for startup) for iOS development
    - A lot of times, projects depend upons specific versions of this IDE. Downloading it from the App Store may not always make a project work, so it's adviced to specify and keep the version used when the app was first created
    - Since you can only download the latest XCode version using the App Store, it's encouraged to use the [Apple Developer Download Site][Apple_Dev_Download] to download a specific version

- [Android Studio][Android_Studio] for Android development
    - Unlike XCode, this IDE doesn't seem to break builds with updates, so it's recomended to keep it, as well as it's interna dependencies, updated. Particularly the emulator

- [Java Developmen Kit][JDK_Info] (Version 11.0.5 used for startup) for CLI Android builds
    - This and version 8 usually works fine. Later versions haven't worked with the current version of React Native
    - As to keep and maintain specific java versions (if necessary), it's recommended to use [jEnv] to manage and install specific versions and switch between them in the machine
    - Open JDKs downloaded from Homebew work just fine

# Local execution

# Generate product

[XCode]: https://developer.apple.com/xcode/
[RN_Dev]: https://reactnative.dev/docs/environment-setup
[Apple_Dev_Download]: https://developer.apple.com/download/all/
[Android_Studio]: https://developer.android.com/studio
[JDK_Info]: https://www.ibm.com/docs/en/i/7.3?topic=platform-java-development-kit
[jEnv]: https://www.jenv.be
[Homebrew]: https://brew.sh
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