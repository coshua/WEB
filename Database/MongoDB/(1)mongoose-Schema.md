## Schema
Since MongoDB has no tables, it could contain almost any types in documents. The problem is it cannot prevent typo or other things users make.
To prevent these things happen and secure a more solid data structure, MongoDB introduces **Schema**. It verifies data users tyring to put into a certain document.

```javascript //User.js
const mongoose = require('mongoose');

const UserSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true,
    unique: true
  },
  date: {
    type: Date,
    default: Date.now
  }
});

module.exports = User = mongoose.model('user', UserSchema);
```

First parameter of **mongoose.model** represents the name of database collection where datas collected with this Schema reside.
In this case, the name of collection would be 'users'.    

In any files, you could import module and use it. `const User = require('../../models/User');`

Useful methods
---
