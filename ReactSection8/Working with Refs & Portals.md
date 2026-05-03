<details>
<summary>Module Introduction & Starting Project</summary>

**Refs & Portals**

*Advanced DOM Access & Value Management*

- Accessing *DOM Elements* with *Refs*
- *Managing Values* with Refs
- *Expossing API Functions* from Components
- *Detaching DOM Rendering* from JSX Structure with *Portals*

Next, just do the command **npm install** from the provided file here : 

https://github.com/academind/react-complete-guide-course-resources/blob/main/attachments/08%20Refs%20Portals/01-starting-project.zip

and then **npm run dev** to know what is inside

<img width="475" height="159" alt="image" src="https://github.com/user-attachments/assets/adac3a56-ca40-403e-bb0b-e34177427de3" />

</details>

<details>
<summary>Repetition : Managing User Input with State (Two Way-Binding)</summary>

In Player.jsx file we can add useState('') with an empty parameter for the first step.

First file of Player.jsx is :

```javascript

export default function Player() {
  return (
    <section id="player">
      <h2>Welcome unknown entity</h2>
      <p>
        <input type="text" />
        <button>Set Name</button>
      </p>
    </section>
  );
}

```

The code of Player.jsx after we add useState and also we should add a function like handleChange() etc.

```javascript
import { useState } from 'react';

export default function Player() {
  const [enteredPlayerName, setEnteredPlayerName] = useState('');
  const [submitted, setSubmitted] = useState(falsee);

  function handleChange(event) {
    setSubmitted(false);
    setEnteredPlayerName(event.target.value);
  }

  function handleClick() {
    setSubmitted(true);
  }

  return (
    <section id="player">
      <h2>Welcome {submitted ? enteredPlayerName : 'unknown entiry'}</h2>
      <p>
        <input type="text" onChange={handleChange} value={enteredPlayerName} />
        <button onClick={handleClick}>Set Name</button>
      </p>
    </section>
  );
}

```

Note : The codes above is not a greate way to write there, will continue in the next lecture.

</details>

<details>
<summary>Repetition : Fragments</summary>

In earlier versions of this course, this section also introduced the concept of "React Fragments" (<Fragment> ... </Fragment> or <> ... </>).

The newer version of the course already introduced this concept in the "React Essentials" sections.

But since it's a key concept that will be used throughout the entire course (and, in general, in pretty much all React projects), it's time for a brief refresher!

When writing JSX code, there's one important rule: A JSX value must have only one root element.

For example, the following code would be invalid and cause an error:

```javascript
return (
  <h2>Welcome!</h2>
  <p>React is awesome!</p>
);
```

So would this code:

```javascript
const content = (
  <h2>Welcome!</h2>
  <p>React is awesome!</p>
);
```

In both snippets, the JSX value has two sibling root elements - and that's not allowed!

One solution would be to wrap these elements into a <div> - which then acts as a single root JSX element:

```javascript
return (
  <div>
    <h2>Welcome!</h2>
    <p>React is awesome!</p>
  </div>
);
```

This would work and therefore is an acceptable solution.

But it has a downside: You now have that extra <div> in your DOM - even though you don't really need it (besides for getting rid of the this error).

That's why React offers a better solution: A special JSX element called "React Fragment".

It can be used as a wrapper to ensure that there's only one root JSX element whilst at the same time not rendering any DOM element.

You can use it like this:

```javascript
import { Fragment } from 'react';
 
// ... other code ...
 
return (
  <Fragment>
    <h2>Welcome!</h2>
    <p>React is awesome!</p>
  </Fragment>
);
```

Most React projects (e.g., projects created with Vite or create-react-app) offer an even shorter form:

```javascript
// no import needed
 
return (
  <>
    <h2>Welcome!</h2>
    <p>React is awesome!</p>
  </>
);
```



</details>
