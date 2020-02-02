1. Change directory:

    ```
    cd
    ```

2. Take step back 1 level:

    ```
    cd ..
    ```

3. List items in current folder:

    ```
    ls
    ls -la
    ```

4. Checking what kind of flags has specific command, e.g.

    ```
    man ls
    ```

    `man `(from manual) is showing you what kind of flags u can use in `ls` command

5. Creating new folder

    ```
    mkdir app
    ```

    for nested folders just add `-p`:

    ```
    mkdir -p app/test
    ```

6. Creating a file

    ```
    touch index.html
    ```

7. Showing graph/tree of your folders

    ```
    tree
    ```

8. Deleting files:

    ```
    rm index.html
    ```

    `rm` is not deleting folders so u should add flag `-rf`

    ```
    rm -rf app
    ```

9. Searching for files:

    ```
    find . -name "README*"
    ```

    `*` =  search for anything after word `README`

10. Cloning existing file

    ```
    cat package.json > package2.json
    ```

    This line is creating new file called `package2.json` and it contains everything from `package.json` file

11. sad

12. ds

13. a

14. dsa

15. 