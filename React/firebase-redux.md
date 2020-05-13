# Fireebase

## Install

1. type this in your project

```shell
npm install firebase@7.8.0
npm install react-redux-firebase@3.1.1 redux-firestore@0.12.0
```

2. setup firebase tools

```shell
npm install -g firebase-tools@7.13.1
```

3. login to firebase CLI

## Firebase Config

1. Make '.env' file for API keys

   ```shell
   REACT_APP_FIREBASE_API_KEY = "YOUR-UNIQUE-CREDENTIALS"
   REACT_APP_FIREBASE_AUTH_DOMAIN = "YOUR-PROJECT-NAME.firebaseapp.com"
   REACT_APP_FIREBASE_DATABASE_URL = "https://YOUR-PROJECT-NAME.firebaseio.com"
   REACT_APP_FIREBASE_PROJECT_ID = "YOUR-PROJECT-FIREBASE-PROJECT-ID"
   REACT_APP_FIREBASE_STORAGE_BUCKET = "YOUR-PROJECT-NAME.appspot.com"
   REACT_APP_FIREBASE_MESSAGING_SENDER_ID = "YOUR-PROJECT-SENDER-ID"
   REACT_APP_FIREBASE_APP_ID = "YOUR-PROJECT-APP-ID"
   ```

2. Make a firebase.js file for config 

   ```javascript
   import * as firebase from 'firebase';
   import 'firebase/firestore';
   
   const firebaseConfig = {
     apiKey: process.env.REACT_APP_FIREBASE_API_KEY,
     authDomain: process.env.REACT_APP_FIREBASE_AUTH_DOMAIN,
     databaseURL: process.env.REACT_APP_FIREBASE_DATABASE_URL,
     projectId: process.env.REACT_APP_FIREBASE_PROJECT_ID,
     storageBucket: process.env.REACT_APP_FIREBASE_STORAGE_BUCKET,
     messagingSenderId: process.env.REACT_APP_FIREBASE_SENDER_ID,
     appId: process.env.REACT_APP_FIREBASE_APP_ID 
   }
   
   firebase.initializeApp(firebaseConfig);
   firebase.firestore();
   
   export default firebase;
   
   ```

3. Update index file

   ```javascript
   import { ReactReduxFirebaseProvider } from 'react-redux-firebase';
   import { createFirestoreInstance } from 'redux-firestore';
   import firebase from "./firebase";
   
   const store = createStore(rootReducer);
   
   const rrfProps = {
     firebase,
     config: {
           userProfile: "users"
       },
     dispatch: store.dispatch,
     createFirestoreInstance
   }
   
   ReactDOM.render(
     <Provider store={store}>
       <ReactReduxFirebaseProvider {...rrfProps}>
         <App />
       </ReactReduxFirebaseProvider>
     </Provider>,
     document.getElementById('root')
   )
   
   ```

## Interact with Firebase

---

```javascript
useFirestoreConnect([ { collection: 'surveys' }, { collection: 'submissions' } ]);


firestoreConnect(() => [
  {
    collection: 'states',
    doc: 'CA',
    subcollections: [
        { collection: 'cities', doc: 'SF' },
        { collection: 'zips' }
      ]
  }
]);
```



## Deploy

1. list projects

   ```shell
   firebase projects:list
   ```

2. Initialize Firebase for your project

   ```shell
   firebase init
   ```

3. Used 'build' as public directory

   ```shell
   npm run build
   ```

4. Run Firebase serve to makesure the site works

   ```shell
   firebase serve
   ```

5. Deploy to Firebase

   ```shell
   firebase deploy
   ```