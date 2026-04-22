<details>
<summary>Module Intorudction & Starting Project</summary>

**Caution** : It's not about CSS lesson

**Styling React Apps**

*Static & Dynamic Styling for Pretty Apps*

- Styling with *Vanilla CSS*
- *Scoping* Styles with *CSS Module*
- *CSS-in-JS* Styling with *Styled Components*
- Styling with *Talwind CSS*
- Static & *Dynamic (Conditional)* Styling

We start the project attached on a course and get ready to install by **npm install** and run as **npm run dev**. And we'll see for a temporary result below but we still can not do anything.

<img width="339" height="424" alt="image" src="https://github.com/user-attachments/assets/eb424291-3688-4f4c-aa1a-d590d694950e" />

</details>

<details>
<summary>Splitting CSS Code Across Multiple Files</summary>

We have a index.css file before, in that file there is a header codes to style on a header file. First step we can separate them into a new file by creating a new component file on a components folder. e.g Header.css

From index.css file in header, we can cut & paste into Header.css file

This is index.css file :

```css
* {
  box-sizing: border-box;
}

html {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto,
    Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

body {
  /* Taken from SVGBackgrounds.com */
  background-color: #ffaa00;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100%25' height='100%25' viewBox='0 0 1600 800'%3E%3Cg %3E%3Cpath fill='%23ffb100' d='M486 705.8c-109.3-21.8-223.4-32.2-335.3-19.4C99.5 692.1 49 703 0 719.8V800h843.8c-115.9-33.2-230.8-68.1-347.6-92.2C492.8 707.1 489.4 706.5 486 705.8z'/%3E%3Cpath fill='%23ffb800' d='M1600 0H0v719.8c49-16.8 99.5-27.8 150.7-33.5c111.9-12.7 226-2.4 335.3 19.4c3.4 0.7 6.8 1.4 10.2 2c116.8 24 231.7 59 347.6 92.2H1600V0z'/%3E%3Cpath fill='%23ffbe00' d='M478.4 581c3.2 0.8 6.4 1.7 9.5 2.5c196.2 52.5 388.7 133.5 593.5 176.6c174.2 36.6 349.5 29.2 518.6-10.2V0H0v574.9c52.3-17.6 106.5-27.7 161.1-30.9C268.4 537.4 375.7 554.2 478.4 581z'/%3E%3Cpath fill='%23ffc500' d='M0 0v429.4c55.6-18.4 113.5-27.3 171.4-27.7c102.8-0.8 203.2 22.7 299.3 54.5c3 1 5.9 2 8.9 3c183.6 62 365.7 146.1 562.4 192.1c186.7 43.7 376.3 34.4 557.9-12.6V0H0z'/%3E%3Cpath fill='%23ffcc00' d='M181.8 259.4c98.2 6 191.9 35.2 281.3 72.1c2.8 1.1 5.5 2.3 8.3 3.4c171 71.6 342.7 158.5 531.3 207.7c198.8 51.8 403.4 40.8 597.3-14.8V0H0v283.2C59 263.6 120.6 255.7 181.8 259.4z'/%3E%3Cpath fill='%23ffd914' d='M1600 0H0v136.3c62.3-20.9 127.7-27.5 192.2-19.2c93.6 12.1 180.5 47.7 263.3 89.6c2.6 1.3 5.1 2.6 7.7 3.9c158.4 81.1 319.7 170.9 500.3 223.2c210.5 61 430.8 49 636.6-16.6V0z'/%3E%3Cpath fill='%23ffe529' d='M454.9 86.3C600.7 177 751.6 269.3 924.1 325c208.6 67.4 431.3 60.8 637.9-5.3c12.8-4.1 25.4-8.4 38.1-12.9V0H288.1c56 21.3 108.7 50.6 159.7 82C450.2 83.4 452.5 84.9 454.9 86.3z'/%3E%3Cpath fill='%23ffef3d' d='M1600 0H498c118.1 85.8 243.5 164.5 386.8 216.2c191.8 69.2 400 74.7 595 21.1c40.8-11.2 81.1-25.2 120.3-41.7V0z'/%3E%3Cpath fill='%23fff852' d='M1397.5 154.8c47.2-10.6 93.6-25.3 138.6-43.8c21.7-8.9 43-18.8 63.9-29.5V0H643.4c62.9 41.7 129.7 78.2 202.1 107.4C1020.4 178.1 1214.2 196.1 1397.5 154.8z'/%3E%3Cpath fill='%23ffff66' d='M1315.3 72.4c75.3-12.6 148.9-37.1 216.8-72.4h-723C966.8 71 1144.7 101 1315.3 72.4z'/%3E%3C/g%3E%3C/svg%3E");
  background-attachment: fixed;
  background-size: cover;
}

button {
  cursor: pointer;
  background: none;
  line-height: inherit;
}

button:focus {
  outline: none;
}

header {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 2rem;
  margin-bottom: 2rem;
}

header img {
  object-fit: contain;
  margin-bottom: 2rem;
  width: 11rem;
  height: 11rem;
}

header h1 {
  font-size: 1.5rem;
  font-weight: 600;
  letter-spacing: 0.4em;
  text-align: center;
  text-transform: uppercase;
  color: #9a3412;
  font-family: 'Pacifico', cursive;
  margin: 0;
}

header p {
  text-align: center;
  color: #a39191;
  margin: 0;
}

@media (min-width: 768px) {
  header {
    margin-bottom: 4rem;
  }

  header h1 {
    font-size: 2.25rem;
  }
}

#auth-inputs {
  width: 100%;
  max-width: 28rem;
  padding: 2rem;
  margin: 0 auto;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
  background: linear-gradient(180deg, #474232 0%, #28271c 100%);
  color: white;
}

.controls {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.controls label {
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #6b7280;
}

.controls input {
  width: 100%;
  padding: 0.75rem 1rem;
  line-height: 1.5;
  background-color: #d1d5db;
  color: #374151;
  border: 1px solid transparent;
  border-radius: 0.25rem;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
}

label.invalid {
  color: #f87171;
}

input.invalid {
  color: #ef4444;
  border-color: #f73f3f;
  background-color: #fed2d2;
}

.actions {
  display: flex;
  justify-content: flex-end;
  gap: 1rem;
}

.button {
  padding: 1rem 2rem;
  font-weight: 600;
  text-transform: uppercase;
  border-radius: 0.25rem;
  color: #1f2937;
  background-color: #f0b322;
  border-radius: 6px;
  border: none;
}

.button:hover {
  background-color: #f0920e;
}

.text-button {
  color: #f0b322;
  border: none;
}

.text-button:hover {
  color: #f0920e;
}

```

This is a Header.css file, on some header code be moved here :

```css
header {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 2rem;
  margin-bottom: 2rem;
}

header img {
  object-fit: contain;
  margin-bottom: 2rem;
  width: 11rem;
  height: 11rem;
}

header h1 {
  font-size: 1.5rem;
  font-weight: 600;
  letter-spacing: 0.4em;
  text-align: center;
  text-transform: uppercase;
  color: #9a3412;
  font-family: 'Pacifico', cursive;
  margin: 0;
}

header p {
  text-align: center;
  color: #a39191;
  margin: 0;
}

@media (min-width: 768px) {
  header {
    margin-bottom: 4rem;
  }

  header h1 {
    font-size: 2.25rem;
  }
}
```

So on Header.jsx file we can add an import from Header.css

```javascript
import logo from '../assets/logo.png';
import './Header.css';

export default function Header() {
  return (
    <header>
      <img src={logo} alt="A canvas" />
      <h1>ReactArt</h1>
      <p>A community of artists and art-lovers.</p>
    </header>
  );
}

```

And the styles on web result is still the same.

</details>

<details>
<summary>Styling React Apps with Vanilla CSS - Props & Cons</summary>

**Vanilla CSS : Advantages & Disadvantages**

**Advantages**

- CSS code is decoupled from JSX code
- You write CSS code as you (maybe) know and (maybe) love it
- CSS code can be written by another developer who needs only a minimal amount of access to your JSX code

**Disadvantages**

- You need to know CSS
- CSS code is not scoped to components --> CSS rules may clash across components (e.g same CSS class name used in different components for different purposes) 
</details>

<details>
<summary>Vanilla CSS Styles are NOT Scoped To Components</summary>

In this case (at Header.css file) for example we remove the header on paraghraph from header p to p

from :

``css
header p {
  text-align: center;
  color: #a39191;
  margin: 0;
}
```

to 

```css
p {
  text-align: center;
  color: #a39191;
  margin: 0;
}
```

and the same time we add demo code on *AuthInputs.jsx* file. e.g we add a paragraph **<p> Some Text </p>** 

```javascript
import { useState } from 'react';

export default function AuthInputs() {
  const [enteredEmail, setEnteredEmail] = useState('');
  const [enteredPassword, setEnteredPassword] = useState('');
  const [submitted, setSubmitted] = useState(false);

  function handleInputChange(identifier, value) {
    if (identifier === 'email') {
      setEnteredEmail(value);
    } else {
      setEnteredPassword(value);
    }
  }

  function handleLogin() {
    setSubmitted(true);
  }

  const emailNotValid = submitted && !enteredEmail.includes('@');
  const passwordNotValid = submitted && enteredPassword.trim().length < 6;

  return (
    <div id="auth-inputs">
      <div className="controls">
        <p>
          <label>Email</label>
          <input
            type="email"
            className={emailNotValid ? 'invalid' : undefined}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        </p>
        <p>
          <label>Password</label>
          <input
            type="password"
            className={passwordNotValid ? 'invalid' : undefined}
            onChange={(event) =>
              handleInputChange('password', event.target.value)
            }
          />
        </p>
      </div>
      <p>Some Text</p>
      <div className="actions">
        <button type="button" className="text-button">
          Create a new account
        </button>
        <button className='button' onClick={handleLogin}>Sign In</button>
      </div>
    </div>
  );
}

```

We try to edit the css code on Header.css and the color become red.

```css
p {
  text-align: center;
  /* color: #a39191; */
  color : red;
  margin: 0;
}
```

We could see that the text of SOme Text become red, but also the text of A Community ..... also become red

<img width="391" height="402" alt="image" src="https://github.com/user-attachments/assets/afc50940-62e9-4e97-8aa2-a921de0436a9" />

</details>

<details>
<summary>Styling React Apps with inline Styles</summary>

To make this clear, we try on Header.jsx file, then we fill on p> paragraph the style with a dinamic style using curly bracess the key enouth or directy typed but the value must be filled by string.

We can see this in inline css style code below :

```javascript
import logo from '../assets/logo.png';
import './Header.css';

export default function Header() {
  return (
    <header>
      <img src={logo} alt="A canvas" />
      <h1>ReactArt</h1>
      <p style={{
        color : 'red',
      }}>A community of artists and art-lovers.</p>
    </header>
  );
}

```

save this and see on web. It's red again :

<img width="308" height="372" alt="image" src="https://github.com/user-attachments/assets/a7df67e5-d980-447b-8976-0c3e19ed9676" />

And also the key can be written as a camelCase character. e.g :

```javascript
<p style={{
        color : 'red',
        textAlign: 'left'
      }}>A community of artists and art-lovers.</p>
```

**Inline Styles : Advantages & Disadvantages**

**Advantages**

- Quick & easy to add to JSX
- Styles only affect the element to which you add them
- Dynamic (conditional) styling is simple

**Disadvantages**

- You need to know CSS
- You need to style every element individually
- No separation between CSS & JSX code

</details>

<details>
<summary>Dynamic & Conditional Inline Styles</summary>

We can remove the inline styles from the Header.jsx file as writen in previous lecture. And now we switch into AuthInputs.jsx file. 

First we command out the codes on AuthInputs.jsx for the code //className={emailNotValid ? 'invalid' : undefined} and we try to input the by inline styles

```javascript
import { useState } from 'react';

export default function AuthInputs() {
  const [enteredEmail, setEnteredEmail] = useState('');
  const [enteredPassword, setEnteredPassword] = useState('');
  const [submitted, setSubmitted] = useState(false);

  function handleInputChange(identifier, value) {
    if (identifier === 'email') {
      setEnteredEmail(value);
    } else {
      setEnteredPassword(value);
    }
  }

  function handleLogin() {
    setSubmitted(true);
  }

  const emailNotValid = submitted && !enteredEmail.includes('@');
  const passwordNotValid = submitted && enteredPassword.trim().length < 6;

  return (
    <div id="auth-inputs">
      <div className="controls">
        <p>
          <label>Email</label>
          <input
            type="email"
            style={{
              backgroundColor: emailNotValid ? '#fed2d2' : '#d1d5db'
            }}
            //className={emailNotValid ? 'invalid' : undefined}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        </p>
        <p>
          <label>Password</label>
          <input
            type="password"
            //className={passwordNotValid ? 'invalid' : undefined}
            onChange={(event) =>
              handleInputChange('password', event.target.value)
            }
          />
        </p>
      </div>
      <div className="actions">
        <button type="button" className="text-button">
          Create a new account
        </button>
        <button className='button' onClick={handleLogin}>Sign In</button>
      </div>
    </div>
  );
}

```
</details>

<details>
<summary>Dynamic & Conditional Styling with CSS Files & CSS Classes</summary>

We command on again the previous code on AuthInputs.jsx file. 

So in the other way, you can add also ternary expression on a label like this 

```javascript
<p>
          <label className={`label ${emailNotValid ? 'invalid' : ''}`}>Email</label>
          <input
            type="email"
            //style={{
              //backgroundColor: emailNotValid ? '#fed2d2' : '#d1d5db'
            //}}
            className={emailNotValid ? 'invalid' : undefined}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        </p>
```
And on Header.css file for a temporary ke can eliminate the code header on p first like this :

```css
p {
  text-align: center;
  color: #a39191;
  /* color : red; */
  margin: 0;
}
```
We can see the details here :

```javascript
import { useState } from 'react';

export default function AuthInputs() {
  const [enteredEmail, setEnteredEmail] = useState('');
  const [enteredPassword, setEnteredPassword] = useState('');
  const [submitted, setSubmitted] = useState(false);

  function handleInputChange(identifier, value) {
    if (identifier === 'email') {
      setEnteredEmail(value);
    } else {
      setEnteredPassword(value);
    }
  }

  function handleLogin() {
    setSubmitted(true);
  }

  const emailNotValid = submitted && !enteredEmail.includes('@');
  const passwordNotValid = submitted && enteredPassword.trim().length < 6;

  return (
    <div id="auth-inputs">
      <div className="controls">
        <p>
          <label className={`label ${emailNotValid ? 'invalid' : ''}`}>Email</label>
          <input
            type="email"
            //style={{
              //backgroundColor: emailNotValid ? '#fed2d2' : '#d1d5db'
            //}}
            className={emailNotValid ? 'invalid' : undefined}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        </p>
        <p>
          <label className={`label ${emailNotValid ? 'invalid' : ''}`}>Password</label>
          <input
            type="password"
            className={passwordNotValid ? 'invalid' : undefined}
            onChange={(event) =>
              handleInputChange('password', event.target.value)
            }
          />
        </p>
      </div>
      <div className="actions">
        <button type="button" className="text-button">
          Create a new account
        </button>
        <button className='button' onClick={handleLogin}>Sign In</button>
      </div>
    </div>
  );
}

```

When we try to click the button and the text is still empty, it would response such this picture below :

<img width="353" height="403" alt="image" src="https://github.com/user-attachments/assets/589ce846-f1b9-49f6-80db-7a9f74022056" />

</details>

<details>
<summary>Scoping CSS Rules with CSS Modules</summary>

**CSS Modules**

Vanilla CSS with file-specific scoping

We can change first the code p element selector in Header.css into element selector paragraph like this :

Before :

```css
p {
  text-align: center;
  color: #a39191;
  /* color : red; */
  margin: 0;
}
```

into :

```css
.paragraph {
  text-align: center;
  color: #a39191;
  /* color : red; */
  margin: 0;
}
```

So in Header.jsx file we can add a className on a paragraph / <p 

```javascript
import logo from '../assets/logo.png';
import './Header.css';

export default function Header() {
  return (
    <header>
      <img src={logo} alt="A canvas" />
      <h1>ReactArt</h1>
      <p className='paragprah'>A community of artists and art-lovers.</p>
    </header>
  );
}

```

also adding on AuthInputs.jsx 

```javascript
  return (
    <div id="auth-inputs">
      <div className="controls">
        <p className='paragraph'>
          <label className={`label ${emailNotValid ? 'invalid' : ''}`}>Email</label>
          <input
            type="email"
            //style={{
              //backgroundColor: emailNotValid ? '#fed2d2' : '#d1d5db'
            //}}
            className={emailNotValid ? 'invalid' : undefined}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        </p>
```

The result on web would be centered for the email label like this :

<img width="281" height="214" alt="image" src="https://github.com/user-attachments/assets/984bab85-45c9-4615-b6ca-e671a1420ce8" />

But how if we rename the file of Header.css into Header.module.css. After renamed we can update the codes on Header.jsx file and update the import area from **import './Header.css** into **import *classes* from './Header.moule.css'**. You have to note that the name of **classes** here is up to you. but commonly given name like that. 

and also update the className={classes.paragraph}. Why adding a paragraph? because we have added paragraph name on css file.

```javascript
import logo from '../assets/logo.png';
import classes from './Header.module.css';

export default function Header() {
  return (
    <header>
      <img src={logo} alt="A canvas" />
      <h1>ReactArt</h1>
      <p className={classes.paragraph}>A community of artists and art-lovers.</p>
    </header>
  );
}

```

If we see on the browser and we inspect the element, we'll se that there's a wrap on <p class="_paragraph_swvrj_28". I'ts the unique codes that's shown on the browser.

</details>



