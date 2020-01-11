[TOC]

# Getting started with hooks

Now we want to make it so you can modify what your search parameters are. Let's make a new route called SearchParams.js and have it accept these search parameters.

```react
import React, { useState } from "react";

const SearchParams = () => {
  // const location = "Seattle, WA";
  const [location, setLocation] = useState("Seattle, WA");         <------- hook

  return (
    <div className="search-params">
      <form>
        <label htmlFor="location">
          location
          <input
            id="location"
            value={location}
            placeholder="Location"
            onChange={e => {
              setLocation(e.target.value);
            }}
          />
          <button type="submit">Submit</button>
        </label>
      </form>
    </div>
  );
};

export default SearchParams;

```

# Unique List Item Keys

```react
import React, { useState } from "react";
import { ANIMALS } from "@frontendmasters/pet";

const SearchParams = () => {
  // const location = "Seattle, WA";
  const [location, setLocation] = useState("Seattle, WA");
  const [animal, setAnimal] = useState("dog");

  return (
    <div className="search-params">
      <form>
        <label htmlFor="location">
          Location
          <input
            id="location"
            value={location}
            placeholder="Location"
            onChange={e => {
              setLocation(e.target.value);
            }}
          />
          <button type="submit">Submit</button>
        </label>
        <label htmlFor="animal">
          Animal
          <select
            id="animal"
            value={animal}
            onChange={e => setAnimal(e.target.value)}
            onBlur={e => setAnimal(e.target.value)}
          >
            <option>All</option>
            {ANIMALS.map(animal => (
              <option 
                  key={animal} 					<-------- it needs to have UNIQUE KEY to show up
                  value={animal}>
                {animal}
              </option>
            ))}
          </select>
        </label>
      </form>
    </div>
  );
};

export default SearchParams;

```

# Effect

# [Handling Async](https://btholt.github.io/complete-intro-to-react-v5/async)

# [Reach Router](https://btholt.github.io/complete-intro-to-react-v5/reach-router)

```
npm install @reach/router
```

## Using Router

```react
// at top
import { Router } from "@reach/router";
import Details from "./Details";

// replace <SearchParams />
<Router>
  <SearchParams path="/" />
  <Details path="/details/:id" />
<Router />;
```

## Usage of Link

```react
// at top
import { Link } from "@reach/router";

// change wrapping <a>
<Link to={`/details/${id}`} className="pet">
</ Link>;
```



# [Class Components](https://btholt.github.io/complete-intro-to-react-v5/class-components)



## componentDidMount

is a function that's called after the first rendering is completed. This pretty similar to a `useEffect` call that only calls the first time. This is typically where you want to do data fetching. 

## static getDerivedStateFromProps

getDerivedStateFromProps does exactly what it sounds like: it allows you to accept data from a parent and get state that is derived from it. In this case, we're removing the superfluous photos and just keeping the ones we want.

```react
  static getDerivedStateFromProps({ media }) {
    let photos = ["http://placecorgi.com/600/600"];

    if (media.length) {
      photos = media.map(({ large }) => large);
    }

    return { photos };
  }
```

# Context



# Redux

