# How to install Tailwindcss

1. Initialize `package.json`:

    ```
    npm init -y
    ```

2. Install tailwind css package from npm:

    ```
    npm install tailwindcss
    ```

3. Create in your project `src` and `public` folder

4. In `src` folder create `styles.css` file and inside put this code:

    ```css
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```

5. Next go to `package.json` and in `scripts` section add

    ```json
    {
    	"scripts": {
    		"build-css": "tailwindcss build src/styles.css -o public/styles.css",
    	}
    }
    ```

6. Next run this line in your terminal

    ```
    npm run build-css
    ```

    Tailwind will proccess `src/style`.css file for us and output it in `public/styles.css` 

    We should have `style.css` file in our `public` folder filled with tallwind classes

7. Now, we can create `index.html` file in `public` folder

# How create config file for Tailwindcss

1. Create blank config file

    ```
    npx tailwindcss init
    ```

    Command creates `tailwind.config.js` and inside it you can find

    ```javascript
    module.exports = {
      purge: [],
      theme: {
        extend: {
        },
      },
      variants: {},
      plugins: [],
    }
    
    ```

2. We can now write our own style in this config, e.g.

    ```javascript
    module.exports = {
      purge: [],
      theme: {
        extend: {
          colors: {
            primary: '#FF6363',
            secondary: {
              100: '#E2E2D5',
              200: '#888883',
            }
          },
        },
      },
      variants: {},
      plugins: [],
    }
    
    ```

    

# 