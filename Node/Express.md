# Popular methods

# How to create route

```javascript
const express = require('express');
const app = express();

app.get('/api', (req, res) => {
  res.send({ name: 'Yoshi' });
});

app.listen(3000);

```

# CRUD

## Deleting example

```javascript
const Ninja = require('../models/ninja'); <----- Model

router.delete('/ninjas/:id', (req, res) => {
  const userID = req.params.id;
  Ninja.findByIdAndDelete(userID).then((result) => res.send(result));
});
```

## Update example

```javascript
router.put('/ninjas/:id', (req, res) => {
  const userID = req.params.id;
  
  Ninja.findByIdAndUpdate(userID, req.body, { new: true })
    .then((ninja) => {
      res.send(ninja);
    })
    .catch((err) => {
      console.log(err);
    });
});
```



# Error handling with middleware

First u can pass `next` method to the catch method

```javascript
router.post('/ninjas', (req, res, next) => {
  const ninja = new Ninja(req.body);
  ninja
    .save()
    .then((result) => {
      res.send(result);
    })
    .catch(next);
});
```

and then create middleware

```javascript
// Error handling Middleware
app.use((err, req, res, next) => {
  res.status(422).send({
    error: err.message,
  });
});
```

