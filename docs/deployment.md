# ioa | *docs/hosting/quickstart

![whoa](./assets/bill-and-teds-father-time.png)

https://firebase.google.com/docs/hosting/quickstart

## wut ❤️ | ioa deploy

Learn to deploy an application from a repository with the [Firebase CLI](https://firebase.google.com/docs/cli).

When working with React, it helps to know exactly where your public `index.html` is relative to the `build/`. As long as you allowed rewrites prompted by [`firebase init`](https://firebase.google.com/docs/hosting/quickstart), then the below representation is accurate with regard to the structure of your firebase.json file located at the root of your ioa directory.

```
// firebase.json
. . .
{
    "target": "raynes",
    "public": "build",
    "rewrites": [
        {
            "source": "/",
            "dynamicLinks": true
        },
        {
            "source": "**",
            "destination": "/index.html"
        }
    ]
}
. . .
```

## How to get started with firebase in the terminal?

0. If you've cloned the repo for the starter code with the following command to get set up and you're not already working with a project, then proceed.

```terminal
$ git clone git@github.com:MichaelRCruz/ioa.git && cd ioa
```

## How to set up hosting in firebase console?

0. If you've navigated to the Firebase console and created a project or changed into one you already have, then proceed.

1. After giving the project a name, enabling Google Analytics, agreeing to the terms and conditions, finally click through to reveal your project's config page.

2. Head to the firebase hosting page in the console. Arrive there via the side menu under Develop and then click Hosting.

3. There, on the hosting landing page click Get Started with hosting by clicking through. You'll be invited to set up the SDK, but not needed. In fact take note of all CLI _suggestions_, but it's okay to continue past.

4. You're done here, but know you can add an additional url on the hosting page if needed.

## How to add an app to a Firebase project?

0. If you've navigated to the project overview page by clicking the settings icon next to "project settings" in the top left, then proceed.

1. In the area titled, "Your Apps" towards the bottom of the screen, select a web app as the type of app. It's the option directly to the right of Android. ❤️

2. Give your app a nickname, try to keep this the same as your app id, and the url name if possible.

3. Check the box to choose hosting for your app, but make sure the selection matches your intended url. The dropdown seems easy to miss at times.

4. Click "register app", note that the SDK is not required at this point.

5. Again, click next, but this time copy the CLI command to your clip board for convenience, move to the next step, then click "Continue to Console." to finish.

#wut ❤️ | Make sure to have the CLI installed for the next section by pasting to the terminal or by using the command below.

```terminal
$ npm install -g firebase-tools
```

️#wut ❤️ | Update your CLI liberally.

For any CLI, when they're new or just out of beta, the updates are more frequent and have more of an impact compared to later updates across the tool's lifetime. There will be a time, when you're pulling your hair out, but forgot to update the CLI. I promise, maybe probably.

Firebase projects are basically Google Cloud Platform (GCP) projects. A project can have _many_ apps, but for _any_ individual app, try to keep it isolated to one project. In other words, try to maintain a set of related apps together in one system to get along with any super system.

For example, you have an Android app, two web apps, and a iOS app. Try to develop these under _one_ project ID.

#wut ❤️ | The project name you chose at the start is _usually_ your project throughout GCP.

For programmers, please remember best practices expecially regarding naming conventions. You'll find that a consistant naming pattern will save you time and energy when reasoning your way through other surfaces of your system within Firebase and GCP. 

#wut ❤️ | Remember, this is a much larger universe with way more stuff racing through orbit. I'll share some advice from a friend, "You can nuke it out of orbit but I don't suggest relying on that."

## How to utilize Firebase CLI?

A more sophisticated project that includes additional Firebase features, will have additonal configuration questions. If you mess up, use git obviously, but also know that you need to make sure the Firebase CLI is _itself_ configured to use your intended project. It's easy.

Set up your CLI by running the following, but be sure you're using the right project and are also authenticated.

#wut ❤️ | The terminal will redirect you, but address the quick privacy question and you'll be on your way.

```terminal
$ firebase login
$ firebase use ioa
```

INSERT VIDEO

0. If you've installed the Firebase CLI or made sure it is updated with `npm install -g firebase-tools`, then proceed.
1. Verify that you're logged in with `firebase login`.
2. Configure Firebase for your project via the CLI by running `firebase init`.
3. Select your options and be sure to define the correct build foldername as "build". Select `yes` for setting up rewrites, and for those working with the ioa clone, select `no` when asked if you would like to overwrite your existing `index.html`.

#wut ❤️ | Remember `ctrl+c` will abort if needed.

## How to write a firebase.json file for React?

0. If you've navigated to your manifest.json file in your text editor to verify that it's well-formed, then proceed.
1. Make sure `public` is set to the same value as the name of your build folder, "build".
2. Make sure `target` has been named appropriately.
3. Make sure your `manifest.json` file looks like this.

```json
{
  "short_name": "ioa",
  "name": "ioa",
  "icons": [
    {
      "src": "favicon.ico",
      "sizes": "192x192",
      "type": "image/png"
    }
  ],
  "start_url": ".",
  "display": "standalone",
  "theme_color": "#000000",
  "background_color": "#ffffff",
  "gcm_sender_id": "103953800507"
}
```

#wut ❤️ | Research the neat stuff manifest.json can do!

## How to serve Firebase locally?

0. If you've remembered to install dependencies by running `npm i`, then proceed.
1. Prepare with `npm run build`, but it takes time sometimes :)
2. Run `firebase serve`. Read the logs. This is your static server usually on 5000
3. Shut down static server via ctrl + c when needed.

## How to using deploy targets in Firebase?

0. If you have an application configured in the Firebase console and also have a web.app binding url, then proceed.
1. Apply a deploy target to a project by running `firebase target:apply hosting ioa ioa`.
2. Deploy by running `firebase deploy --only hosting:ioa`
3. Visit ioa.web.app

The duplication of `ioa` in the above step is intentional. One represents the binding url and the other represents the app nickname.

#wut ❤️ | [...to be continued.](https://wut.app)
