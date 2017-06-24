# JAVASCRIPT
--- 


### Setup Rest API using Express to login using username/password and JWT

Important note:  If your secret is known, your entire system will be compromised.  Try to store very little data in the jwt payload. 

**Install packages**
```sh
$ npm i --save jsonwebtoken mongoose passport passport-jwt passport-local passport-local-mongoose cookie-parser body-parser
```

**Setup Express**

`./app.js`
Connect to MongoDB, configure passport to use local strategy (username and password), and configure passport to use JWT

```js
// connect to database
var mongoose = require('mongoose');
var db = process.env.MONGO_URL || 'localhost/your-mongodb-name'
mongoose.connect(db);
mongoose.connection.on('error', function() {
    console.info('Error: Could not connect to MongoDB. Did you forget to run `mongod`?')
});

var passport = require('passport');
var LocalStrategy = require('passport-local').Strategy;
var JwtStrategy = require('passport-jwt').Strategy;
var ExtractJwt = require('passport-jwt').ExtractJwt;
var User = require('./models/user');

// Configure Passport to use local strategy for initial authentication.
passport.use('local', new LocalStrategy(User.authenticate()));

// JWT configuration
 var options = {}
   options.jwtFromRequest = ExtractJwt.fromAuthHeader();
   options.secretOrKey = 'your-jwt-secret'

// Configure Passport to use JWT strategy to look up Users.
passport.use('jwt', new JwtStrategy(options, function(jwt_payload, done) {
  //console.log('jwt_paylog: ' + jwt_payload);
  User.findOne({
    _id: jwt_payload.id
  }, function(err, user) {
    if (err) {
      return done(err, false);
    }
    if (user) {
      done(null, user);
    } else {
      done(null, false);
    }
  })
}));
```

`./models/user.js`:
PassportLocalMongoose providers helpers to create and login users, it will also hash and salt passwords.

```js
var mongoose = require('mongoose');
var Schema = mongoose.Schema;
var passportLocalMongoose = require('passport-local-mongoose');

// passport-local-mongoose will add a username, hash and salt field to the User Schema
var User = new Schema({});

// See passport-local-mongoose docs for schema customization options
// https://github.com/saintedlama/passport-local-mongoose#options
User.plugin(passportLocalMongoose, {
  usernameField: 'email',
  usernameUnique: true
});

module.exports = mongoose.model('User', User);
```

`./routes/users.js`:
```js
var express = require('express');
var router = express.Router();
var User = require('../models/user');
var passport = require('passport');
var jwt = require('jsonwebtoken');

var secret = 'your-jwt-secret';

router.post('/login', function(req, res, next) {
    passport.authenticate('local', function(err, user, info) {
        if (err) {
            return next(err);
        }
        if (!user) {
            return res.status(401).json({
                error: 'Invalid credentials.'
            });
        }
        if (user) {
            var token = jwt.sign({
                id: user._id,
                email: user.email    //you can remove this
            }, secret);
            return res
                .status(200)
                .json({
                    token
                });
        }
    })(req, res, next);
});
```

`./routes/index.js`:
```js
var express = require('express');
var router = express.Router();
var passport = require('passport');

router.get('/protected-route', function(req, res, next) {
    passport.authenticate('jwt', function(err, user, info) {
        if (err) {
            // internal server error 
            return next(err);
        }
        if (!user) {
            // no JWT or user found
            return res.status(401).json({
                error: 'Invalid credentials.'
            });
        }
        if (user) {
            // authentication success!
            return res
                .status(200)
                .json({
                    secret: 'hello world '
                });
        }
    })(req, res, next);
});
```
