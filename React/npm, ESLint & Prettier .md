# [npm](https://btholt.github.io/complete-intro-to-react-v5/eslint-prettier)

1) First u have to check if u have node and npm:

```
node -v
npm -v
```

2) In folder of your project. Flag -y means that u skip all question about this file.

```
npm init -y
```

it will give your a package.json, e.g.:

```javascript
{
  "name": "adopt-me",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}

```

# [Prettier](https://btholt.github.io/complete-intro-to-react-v5/eslint-prettier)

```
npm install -D prettier
or
npm i -D prettier
```

-D means Developer dependencies, so when i am deploying my code to production I dont need to go Prettier with it. It is just for me for my local environment.

In package.json we are adding in script tag:

```json
"scripts": {
    "format": "prettier \"src/**/*.{js,html}\" --write",
 },
```

It will run prettier on any file in src folder which has either js extension or html

In Settings of VSCode (Ctrl + , ) you have to set up 2 things:
	1) Format on save -> checked
	2) Require Config -> checked          this will only run prettier when u install it on your project. So when u get other project when there is not prettier u wont break it

Next you have to create file in root folder called.
**.prettierrc**
in this file you have to create empty object and save it. 

```
{}
```

Empty Object means that u want default settings of Prettier

# [ESLint](https://btholt.github.io/complete-intro-to-react-v5/eslint-prettier)

```
npm install -D eslint eslint-config-prettier
```

eslint-config-prettier       <-- means that prettier takes charge over eslint in things like spaces.

then create new file called:
**.eslintrc.json**
inside we can make rules:

```json
{
  "extends": ["eslint:recommended", "prettier", "prettier/react"],
  "plugins": [],
  "parserOptions": {
    "ecmaVersion": 2018,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "env": {
    "es6": true,
    "browser": true,
    "node": true
  }
}
```

in package.json we are adding:

```json
"scripts": {
    "lint": "eslint \"src/**/*.{js,jsx}\" --quiet",
 },
```

Then we should install ESLint Dirk Baeumer from VSCode extensions

## JSX problem

In line 9-15 JSX cant see REACT markup (e.g. React.createElement("h1", {}, name)) so its throw an Error that `React is defined but never used. eslint(no-unused-vars)[1,8]`. 

```react
import React from "react";

export default function Pet({ name, animal, breed }) {
  // return React.createElement("div", {}, [
  //   React.createElement("h1", {}, name),
  //   React.createElement("h2", {}, animal),
  //   React.createElement("h2", {}, breed)
  // ]);
  return (
    <div>
      <h1>{name}</h1>
      <h2>{animal}</h2>
      <h2>{breed}</h2>
    </div>
  );
}

```

We need to give ESLint a hand to get it to recognize React and not yell about React not being used. Right now it thinks we're importing React and not using because it doesn't know what to do with React. Let's help it. Run this:

```command
npm install -D babel-eslint eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react
```

Update your .eslintrc.json to:

```json
{
  "extends": [
    "eslint:recommended",
    "plugin:import/errors",
    "plugin:react/recommended",
    "plugin:jsx-a11y/recommended",
    "prettier",                <-------- has to be at the end
    "prettier/react"			 <-------- has to be at the end
  ],
  "rules": {
    "react/prop-types": 0,
      "no-console": 1
  },
  "plugins": ["react", "import", "jsx-a11y"],
  "parserOptions": {
    "ecmaVersion": 2018,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "env": {
    "es6": true,
    "browser": true,
    "node": true
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  }
}
```

## Configuring ESLint for Hooks

```
npm install -D eslint-plugin-react-hooks
```

Add this to ESLint:

```json
{
  "rules": {
    …,
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": 1
  },
  "plugins": [
    …,
    "react-hooks"
    ],
}
```



# [gitignore](https://btholt.github.io/complete-intro-to-react-v5/eslint-prettier)

```
node_modules/
.DS_Store
.cache/
dist/
coverage/
.vscode/
.env
```

# [Parcel](https://btholt.github.io/complete-intro-to-react-v5/parcel)

1) Install Parcel by doing 

```
npm install -D parcel-bundler
```

2) Now inside of your `package.json` put:

```json
"scripts" {
  "dev": "parcel src/index.html"
}
so should look like this:
"scripts": {
    "dev": "parcel src/index.html",
    "format": "prettier \"src/**/*.{js,html}\" --write",
    "lint": "eslint \"src/**/*.{js,jsx}\" --quiet",
    "test": "echo \"Error: no test specified\" && exit 1"
},
```

3) after running `npm run dev` Parcel is creating dist and .cache folders (ignore it)

4) We can enter to the website by http://localhost:1234/

It is autorefreshing bundler, so if u press SHIFT+S it refreshes site automatically.

5) To stop server from running just press `CTRL + C`

# Babel + Parcel configuration for Constructor

The constructor is annoying. We can use something called class properties to make it a lot nicer and easier to ready. Class properties are an upcoming part of JavaScript so we need to tell Parcel to include that code transformation when it transpiles our code. We do that by making a [Babel](https://babeljs.io/) config file. Babel is the actual library that does the code transformation.

```
npm install -D babel-eslint @babel/core @babel/preset-env @babel/plugin-proposal-class-properties @babel/preset-react
```

Now make a file called `.babelrc` with the following:

```json
{
  "presets": ["@babel/preset-react", "@babel/preset-env"],
  "plugins": ["@babel/plugin-proposal-class-properties"]
}
```

Add one line to the top level of your `.eslintrc.json`:

```json
{
  …
  "parser": "babel-eslint",
  …
}
```

Now with this, we can modify Details to be as so:

```react
// replace constructor
state = { loading: true };
```

# React

```
npm install react react-dom
```

This will pull React and ReactDOM down from npm and put it in your node_modules directory. Now instead of loading them from unpkg, we can tell Parcel to include them in your main bundle. Let's do that now.

## importing

```react
import React from "react";
import { render } from "react-dom";
```

















