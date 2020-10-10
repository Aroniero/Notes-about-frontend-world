Example of using Render Props:

```react
import React from "react";

const MyComponents = (props) => (
  <div>
    <h1>Hello Roman</h1>
    {props.render('Aroniero')}
  </div>
);

const Patterns = () => (
  <div>
    <h2 className="title is-3">Patterns</h2>
    <MyComponents 
        render={(name) => <h2> Hello {name}</h2> }
    />
  </div>
);

export default Patterns;
```

Another use case of Render props:

```react
import React from "react";

const MyComponents = ({ children }) => (
  <div>
    <h1>Hello Roman</h1>
    {children("Yolo")}
  </div>
);

const Patterns = () => (
  <div>
    <h2 className="title is-3">Patterns</h2>
    <MyComponents>
        {(name) => <p>Hello {name}</p>}
     </MyComponents>
  </div>
);

export default Patterns;
```

