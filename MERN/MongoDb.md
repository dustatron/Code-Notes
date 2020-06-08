[atlas](https://www.mongodb.com/cloud/atlas)

uO1l1#8!Rcra

logged in with Google Login as old login broke. 

Mern db
dustymccord
krW9tDWCQrBWBhmF

connect

mongodb+srv://dustymccord:krW9tDWCQrBWBhmF@devconnector-ijcnx.mongodb.net/test?retryWrites=true&w=majority

New link
mongodb+srv://dustymccord:dustymccord@devconnector-mwo0k.mongodb.net/test?retryWrites=true&w=majority



## Install Commands

general pages

```shell
npm i express express-validator bcryptjs config gravatar jsonwebtoken mongoose request
```

Nodemon and concurrently

```
npm i -D nodemon concurrently
```



## Create Mongo DB

1. Create a project.

2. Create a Cluster

3. Add a user to the database

4. add IP address to network access

   1. click add current IP address

   2. or add 0.0.0.0 to allow all traffic

      

## Wire Up Mongoose

#### Make a /models/Profile.js 

```javascript
const mongoose = require('mongoose');

const ProfileSchema = new mongoose.Schema({
  user: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'user',
  },
  otherDetails: {
    goesHere: true
  }
})

module.exports = Profile = mongoose.model('profile', ProfileSchema);
```



This will allow for importuning schemas and mongoose methods on the schema. 

__In your js file where you plan on saving data__

#### In your /routes/profile.js

```javascript
const express = require('express');
const router = express.Router();
const auth = require('../../middleware/auth');

const Profile = require('../../models/Profile');

// @route   POST api/Profile/
// @Desc    Create or update a user profile
// @access  Private

//auth is middleware
router.post('/', auth, async (req, res) => {
  const profileFields = // this is the object you want to save. 
        
   profile = new Profile(profileFields);
   await profile.save();
})

module.exports = router;
```

