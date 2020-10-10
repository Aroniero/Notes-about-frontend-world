# React Router

1. Installing React router:

    ```
    npm install react-router-dom
    ```

2. Importing <BrowserRouter />

    ```react
    import { BrowserRouter } from 'react-router-dom';
    ```

3. Importing <Switch> and <Route>

    ```react
    import { Switch, Route } from 'react-router-dom';
    ```

    <Switch> unables showing this Routes which are fulfilling "path". 

4. Usage:

    ```react
    <BrowserRouter>
          <MainTemplate>
            <Switch>
              <Route exact path="/" render={() => <Redirect to="/notes" />} />
              <Route path="/notes" component={Notes} />
              <Route path="/articles" component={Articles} />
              <Route path="/twitters" component={Twitters} />
            </Switch>
          </MainTemplate>
        </BrowserRouter>
    ```

    ## Dynamic Routes

    

    

    ## NavLink

    1. One of the best thing in `NavLink ` is that u can use `activeclass` on your component so it looks like this:

        ```react
        <ButtonIcon as={NavLink} to="/" icon={penIcon} activeclass="active" />
        <ButtonIcon as={NavLink} to="/twitters" icon={twitterIcon} activeclass="active" />
        <ButtonIcon as={NavLink} to="/articles" icon={bulbIcon} activeclass="active" />
        ```

          It will add automatically the `active` class to component u have clicked.

    

    

# React Redux

1. Installing Redux

    ```
    npm install redux react-redux
    ```

2. das

3. dsa

4. sd

5. sd

6. 

