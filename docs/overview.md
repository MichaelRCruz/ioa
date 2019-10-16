# **ioa | overview**

![whoa](./assets/69dudeswhoa.png)

> "If you guys are really us, then what number are we thinking of?" ~ Ted (Theodore) Logan

## authentication

Consider a stripped down representation of two functions that live inside ioa's top-level context. ioa values a fully isolated authentication process which creates a redeemable session available when revisiting an app.

[future reference](https://firebase.google.com/docs/auth/web/auth-state-persistence#modifying_the_auth_state_persistence)

A special listener, `onAuthStateChanged()`,  inside the app's highest level context provider is tasked with handling all changes to the listener's callback, `user`. It's responsive to a set of well-defined auth state changes, e.g., user chooses to identify with Google or chooses to identify with GitHub, etc.

The following snippet is a representation of ioa initialization. 

```javascript
// src/SessionProvider.js
. . .

componentDidMount() {
  . . .
  const unsubscribe = firebase.auth()
    .onAuthStateChanged(async user => {
      if (user != null) {
        const { providerData, ...rest } = user;
        . . .
        if (userConfig) {
          // initialize with existing user
          this.initializeApp();
        } else {
          // initialize with newly-created config fetched from cloud
          const payload = await api.createNewUser();
          this.initializeApp(payload);
        }
      } else {
        firebase.auth().signOut();
      }
    });
};

. . .
```
Here is a representation of setting the state inside ioa's Provider. Note that all listeners are set by the callback of `setState()` to conclude the Provider's lifecycle.

**Please know that very strict measures are taken in an attempt to limit ioa to only one state change per component.**

```javascript
// src/SessionProvider.js
initializeApp = async () => {
  . . .
  // insert sequence of "blocked" async reduction building initial state
  // memoization?
  this.setState({}, () => {
    // please note these conditions throughout the app.
    // please practice building idempontent operations
    if (user) this.setListeners();
    if (user) this.initNotifications();
  });
};
```

## context

In theory this approach limits to one redraw on initialization, and _only_ reacts to a healthy auth `state` object. Healthy as in well-formed or is null. This destructures down to the respective "global-like" context. The values, `fcmToken` & `user`, will likely be cut in favor of a more secure space. In fact, a revisit to _all_ levels of state is required to sniff out any adjacent and overlooked sources of truth. 

```javascript
// representation of state in SessionProvider.js (will change name of context)

const state = {
  activeRoom,
  fcmToken,
  messages,
  subscribedRooms,
  user,
  userConfig,
  userConfigs
};
```

Some complexity can be removed here, but the context's state redundancies that _will_ remain are minimal and the convenience has been worth it so far. The largest benefit is the help that it provides in avoiding "prop drilling" which ultimately limits the number of redraws throughout the DOM as further described in other sections. Makes for a cool cpu 😎.

