# Opt Out

[![CircleCI](https://circleci.com/gh/opt-out-tools/opt-out.svg?style=svg)](https://circleci.com/gh/opt-out-tools/opt-out) [![Contributor Code Of Conduct](https://img.shields.io/badge/Code%20Of%20Conduct-v1.4%20adopted-ff69b4.svg)](CODE_OF_CONDUCT.md)

Opt Out is a browser extension for Firefox that filters online misogyny from an individual’s twitter feed.

The General Data Protection Regulation (GDPR) has changed our lives online on social media platforms. We have the right to be forgotten, to see what is being collected about us and to opt-out if we wish. The current abuse that those who identify as women suffer is not avoidable. We see Opt Out as an extension of the GDPR that also protects the human rights of women and those with intersecting identities online. While steps have been made to protect these people online, not enough has been done. This is a global tragedy affecting the well-being, economical potential and political representation of these people. Let's **Opt Out.**

Please see the [theory](https://github.com/opt-out-tools/theory-of-online-misogyny) repository, to see our research about this problem.

Opt Out is an open source project under active development. Currently, machine learning models are being evaluated for their ability to classify sexual harassment text. If you would like to test the current model (trained on troll data), please see the 'Installation Instructions' below. If you would like to contribute to the project, please see [Contributing](https://github.com/opt-out-tools/start-here/blob/master/CONTRIBUTING.md) first, and then check out the find-out and try-out repos. Please note that this project is released with a [Contributor Code of Conduct](https://github.com/malteserteresa/opt-out/blob/master/CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

## Development

### Run local development environment

```
npm run start:firefox
```

### Debugging tips

Check out these debugging tips at the [Mozilla Extension Workshop](https://extensionworkshop.com/documentation/develop/debugging/).

#### Force reload webpack build

The module hot-refreshes the browser when there is a change in the source code. To force an update in the browser, press `r` in the terminal where web-ext is running.

#### Keep the popup window open

1. In firefox, open `about:debugging`
2. Go to 'This firefox'
3. Click 'Inspect' next to Opt-Out
4. The dev tools for the popup will open in a new tab
5. **Click the three horizontal dots on the right side**
6. Disable Popup Autohide.

This will keep the popup open unless you press `Esc`, which makes it possible to debug the HTML of the Popup as if it were a static website.

#### Persisting settings on dev browser

To persist your twitter login data after stopping the process, follow these instructions:

- Create a new profile on firefox (at `about:profiles`)
- Open an instance of firefox as this profile
  - `firefox --new-instance -p your_profile_name`
- Sign in to twitter in the browser that opens, you can then close the browser
- Run the development environment start command with a flag to point to this profile.
  - `npm run start:firefox -- -p=your_profile_name`

**Important** Make sure that you do not choose a 'default' profile, such as the profile you use for your personal browsing. Here's why

> This option makes the profile specified by --firefox-profile completely insecure for daily use. It turns off auto-updates and allows silent remote connections, among other things. Specifically, it will make destructive changes to the profile that are required for web-ext to operate.

### Development Guidelines

Please:

- Join the slack if you're planning to contribute
- Keep pull requests isolated to one feature.
- Explain the changes made and how to test it in the PR description
- Ask for help on the slack or on github if needed

## More instructions

### Building for production

To build for production, simply run `npm run build:prod`.

The project will be bundled by webpack in production mode, and `web-ext` will build that project in to a zip file, which can be uploaded to the Mozilla Add Ons site.

### Adding a local pre-commit hook

In case you want to be 100% sure that the linter is always running before you commit you can add this as a [git hook](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks).
This means it will run the linter before every commit you try to make:

#### The easy way:

If you do not have a pre-commit hook defined yet, there is a script that will copy the file for you.
Run this command and it will create the pre-commit from a template for you:

```
npm run git:initHook
```

If you already have a pre-commit hook defined but don't care about overwriting it, you can use the same command with the `-f` flag.
This will copy the template even if the file exists already.

```
npm run git:initHook -f
```

#### The slightly harder way

1. Open the file `.git/hooks/pre-commit`
2. If the file does not exist, create it.
3. Add the following to the file and save it:

```
npm run lint
RESULT=$?
[ $RESULT -ne 0 ] && exit 1
exit 0
```
