# Connection to MongoDb

```javascript
const apiURI =
  'mongodb+srv://tutorial_user:tutorialuserpass@nodetuts.sdxfa.mongodb.net/nodetuts?retryWrites=true&w=majority';

mongoose
  .connect(apiURI, { useNewUrlParser: true, useUnifiedTopology: true })
  .then((result) => app.listen(3000))
  .catch((err) => console.log(err));
```

# Schema

## Creating schema

```javascript

const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const blogSchema = new Schema(
  {
    title: {
      type: 'string',
      required: true,
    },
    snippet: {
      type: 'string',
      required: true,
    },
    body: {
      type: 'string',
      required: true,
    },
  },
  { timestamps: true }
);

const Blog = mongoose.model('Blog', blogSchema);

module.exports Blog

```

## Using Schema

```javascript
const Blog = require('./models/blog');

app.get('/add-blog', (req, res) => {
  const blog = new Blog({
    title: 'Title of 1 blog',
    snippet: 'snippet of 1 blog',
    body: 'more about 1 blog',
  });
  
  blog
    .save()
    .then((result) => {
      res.send(result);
    })
    .catch((err) => {
      console.log(err);
    });
});
```

Better use of blog schema  

```javascript
app.get('/blogs', function (req, res) {
  Blog.find()
    .then((result) => {
      res.render('index', { title: 'Home', blogs: result });
    })
    .catch((err) => {
      console.log(err);
    });
});
```

