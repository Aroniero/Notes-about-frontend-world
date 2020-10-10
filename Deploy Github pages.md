1. Create repository on Github Pages:
    a. Insert `Repository name` of your repository
    b. Click `Create repository` button
    c. Stay on configuration page at the moment. It will be helpful in a second

2. Install gh-pages as dev dependency:

    ```
    npm install gh-pages --save-dev
    ```

    After installation check if you have `gh-pages` in devDependencies in `package.json` file.

3. In `package.json` add:

    ```json
    {
      "homepage": "https://name-of-your-Acc.github.io/name-Of-Your-Repo",  
        // Information for your link you can take from Configuration page.
    }
    ```

    For example

    ```
    {
      "homepage": "https://Aroniero.github.io/nameOfYourRepo", 
    }
    ```

4. Next in the same file (`package.json`) add this script tags:

    ```
    {
       "scripts": {
          "predeploy": "npm run build",
          "deploy": "gh-pages -d build",
       },
    }
    ```

5. Go back to the configuration page of your Github Repository and then do following steps:
    In case you dont have existing project:

    ```
    echo "# github-user-finder" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/Aroniero/github-user-finder.git
    git push -u origin master
    ```

    In case if you want push already existing project

    ```
    git remote add origin https://github.com/Aroniero/github-user-finder.git
    git push -u origin master
    ```

    

6. sda

7. sda

8. 

