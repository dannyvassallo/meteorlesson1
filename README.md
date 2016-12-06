#MeteoReddit

The fastest built reddit clone you've ever seen homie.

####What's in it?

* Meteor
* Iron Router
* Blaze
* AccountsUI
* scss
* materialize-scss
* useraccounts Materialize
* browser-policy
* alanning:roles
* cunneen:accounts-admin-materializecss

####Getting Started

First, we Install [meteor](https://www.meteor.com/install). Second, we start er' up.

NOTE: If you have problems with ANYTHING on windows, try using CMS or PowerShell instead of gitbash to start your meteor instance.

```shell
meteor create myredditclone
cd myredditclone
touch README.md
npm install
meteor run #or meteor
```

Start tracking on github. Like, now.
Visit `localhost:3000` in your browser.
To use robomongo, connect to port `3001`
To use minimongo console, type `mongo` in the
terminal while in the `myredditclone` dir.

![Alt meteor](https://s3-us-west-2.amazonaws.com/meteoreddit/meteor1.png)

Meteor will livereload EVERYTHING. Enjoy that.

####Adding Dependencies Up Front

Meteor has it's own package system called [Atmosphere](https://atmospherejs.com/) that installs
dependencies to `./meteor/package` using `meteor add <dep name>`. You can also use `npm i -S <package name>` to get node modules. You would import node modules the same way you are used to. Meteor packages are automatically available.

Let's get our dependencies installed.
copy paste the following into the bottom
of `./meteor/packages` (bypassing the `meteor add` or `npm install` step.)

```
fourseven:scss
poetic:materialize-scss
useraccounts:materialize
useraccounts:core
useraccounts:iron-routing
accounts-password@1.3.1
browser-policy@1.0.9
browser-policy-common@1.0.11
browser-policy-content@1.0.12
browser-policy-framing@1.0.12
alanning:roles
cunneen:accounts-admin-materializecss
```

We get Scss, materialize-scss, useraccounts (for authentication), Roles (for authorization), browser-policy (for CORS), and an admin panel for account control.

Delete the following lines from the packages file as well:

```
autopublish@1.0.7             # Publish all data to the clients (for prototyping)
insecure@1.0.7                # Allow all DB writes from clients (for prototyping)
```

As a final step run `meteor npm install --save bcrypt`.

####Create An Index Route and a Layout

Lets create an Iron Router. In the root of your project, make a new folder called `lib`. In the lib folder, make a `router.js` and paste in the following:

```javascript
// In the configuration, we declare the layout, 404, loading,
// navbar, and footer templates.
Router.configure({
  layoutTemplate: 'masterLayout',
  loadingTemplate: 'loading',
  notFoundTemplate: 'notFound',
  yieldTemplates: {
    navbar: {to: 'navbar'},
    footer: {to: 'footer'},
  }
});

// In the map, we set our routes.
Router.map(function () {
  // Index Route
  this.route('home', {
    path: '/',
    template: 'home',
    layoutTemplate: 'masterLayout'
  });
});
```

After you've saved the router, goto `localhost:3000`. You should see "Couldn't find a template named "masterLayout" or "masterLayout". Are you sure you defined it?" in red. That's ok.
