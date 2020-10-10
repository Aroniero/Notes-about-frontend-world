# Linters

## Eslint



1. Create `.eslintrc` file in `src` folder of our app

2. Cut out eslint dependency in `package.json` file and paste it into `.eslintrc`:

    ```json
    {
      "extends": "react-app"
    }
    ```

3.  There is a lot of eslint configs. In this example we are using [`eslint-config-airbnb`](https://www.npmjs.com/package/eslint-config-airbnb):

    ```
    npx install-peerdeps --dev eslint-config-airbnb
    ```

4. dasł

5. dsa

6. dsa

sda



## Husky

1. `npm install -D husky lint-staged`

## Lint-staged



# Global paths

Main purpose of Global styles is that we don't want to make path's look like this 

```react
import Root from './views/Root/Root';
```

 Instead we want path's to look like this:

```react
import Root from 'views/Root/Root';
```

So we have to make few steps to create that: 

1. Create `.env` file and add there:

    ```
    NODE_PATH=src
    ```

2. Then our eslint probably wont understand this kind of path so we add settings to our `.eslintrc` file:

    ```json
    {
        "settings": {
            "import/resolver": {
                "node": {
                    "extensions": [".js", ".jsx", ".ts", ".tsx"],
                    "moduleDirectory": ["node_modules", "src/"]
                }
            }
        }
    }
    ```

# Styled-components

## Theme-provider



# [Atomic design](https://bradfrost.com/blog/post/atomic-web-design/)

