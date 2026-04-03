# Module Introduction
## React Essentials Deep Dive
**Beyond The Basics**
- Behind the scenes of JSX
- Structuring **Components** and **State**
- **Advanced State** Usage
- **Patterns & Best Practices**

# You Don't Have To Use JSX!
In previous section (section 3) on file of index.jsx we should edit the of react import from the code :
```javascript
import ReactDOM from 'react-dom/client';
import App from './App';
import './index.css';

const entryPoint = document.getElementById("root");
ReactDOM.createRoot(entryPoint).render(<App />);
```

```md
And the code become :
```
```javascript
import React from 'react';
import App from './App';
import './index.css';

const entryPoint = document.getElementById("root");
//ReactDOM.createRoot(entryPoint).render(<App />);
ReactDOM.createRoot(entryPoint).render(React.createElement(App));
```

# 💡Working with Fragments
First step here on App.jsx we can add fragments on import 
```javascript
import { useState, Fragment } from 'react';
```
```md
and then the <div></div> on code after return ( we can replace by <Fragment></Fragment>

from :
```
```javascript
return (
    <div>
      *... codes*
      </main>
    </div>
```
```md
to :
```
```javascript
return (
    <Fragment>
    <Header />
    <main>
     *.... codes*
    </main>
    </Fragment>
```
