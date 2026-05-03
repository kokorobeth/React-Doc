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

Note : The codes above it not a greate way to write there, will continue in the next lecture.

</details>
