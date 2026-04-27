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

**CSS Module : Advantages & Disadvantages**

**Advantages**

- CSS code is decoupled from JSX code
- You write CSS code as you maybe know and maybe love it
- CSS code can be written by another developer who needs only a minimal amount of access to your JSX code
- CSS classes are scoped to the component files which import them --> No CSS class name clashes

**Disadvantages**

- You need to know CSS
- You may end up with many relatively small CSS files in your project

</details>

<details>
<summary>Introducing "Styled Components" (Third-party Package)</summary>

We now explore about styled components, we can visi the website or just type key search on the browser **styled components** or we can visi https://styled-components.com/

In that there some css file components packages. With that, we can install it by using command :

```html
npm install styled-components
```

So in AuthInputs.jsx file we can update the codes and import like **import { styled } from 'styled-components'**, name styled after import is commonly used, but we can free named as we want. And adding styled.div`` (with backtick) for example. Also actually we can add styled.p etc.

And we go back to index.css file, copy the code below (which inclued of .control) into AuthInputs.jsx file on styled.div ` `

```css
.controls {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}
```

Note : .control is not copied

So paste in AuthInputs.jsx file into :

```css
const ControlContainer = display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
```
And still in AuthInputs.jsx we can replace the code **<div className="controls"** into **<ControlContainer>=== codes are here ===</ControlContainer**

```javascript
import { useState } from 'react';
import { styled } from 'styled-components';

const ControlContainer = styled.div`
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
`

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
      <ControlContainer >
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
      </ControlContainer>
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

Note : When we check on the browser, the results are still not proper, but for a while we check and inspect the codes, there is a unique code that wrapped and secured 

And the codes of div on inspect element become **<div class="sc-gsTDHW djHafr"**

</details>

<details>
<summary>Creating Flexible Components with Styled Components</summary>

In AuthInputs.jsx file we can make a modify again especially in a label by making a variable of label in it

We can copy & paste the codes from index.css for a label into AuthInputs.jsx file

```css
.controls label {
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #6b7280;
}
```

paste in AuthInputs.jsx file

```javascript
const Label = styled.label`
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #6b7280;
`
```

After that we can change the label symbol in the code below :

```javascript
<label className={`label ${emailNotValid ? 'invalid' : ''}`}>
Email
</label>

<Label className={`label ${emailNotValid ? 'invalid' : ''}`}>
Password
</Label>
```

into :

```javascript
<Label className={`label ${emailNotValid ? 'invalid' : ''}`}>
`Email
</Label>

===another codes is here ===

<Label className={`label ${emailNotValid ? 'invalid' : ''}`}>
  Password
</Label>

```

So if we take a look on a website after we do a npm run dev, it looks good again. But there's something to fix afterwards. Yet the style input is still broken. So the we need to make a constant again on AuthInputs.jsx file.

And again we need to copy and paste the codes from index.css file into constant code in AuthInputs.jsx file. Such this codes :

```css
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
```

paste them into :

```javascript
const Input = styled.input`
  width: 100%;
  padding: 0.75rem 1rem;
  line-height: 1.5;
  background-color: #d1d5db;
  color: #374151;
  border: 1px solid transparent;
  border-radius: 0.25rem;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
`
```

And we also change the <input element into <Input. As we can see below :

```javascript
<Input
            type="email"
            //style={{
              //backgroundColor: emailNotValid ? '#fed2d2' : '#d1d5db'
            //}}
            className={emailNotValid ? 'invalid' : undefined}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        </p>
        <p>
          <Label className={`label ${emailNotValid ? 'invalid' : ''}`}>
            Password
          </Label>
          <Input
            type="password"
            className={passwordNotValid ? 'invalid' : undefined}
            onChange={(event) =>
              handleInputChange('password', event.target.value)
            }
          />
```

We see on the browser, the display prettier again :

<img width="347" height="419" alt="image" src="https://github.com/user-attachments/assets/19828977-e144-4c14-b224-b11ac19ddd86" />



And here is the complete codes of AuthInputs.jsx file 

```javascript
import { useState } from 'react';
import { styled } from 'styled-components';

const ControlContainer = styled.div`
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
`

const Label = styled.label`
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #6b7280;
`

const Input = styled.input`
  width: 100%;
  padding: 0.75rem 1rem;
  line-height: 1.5;
  background-color: #d1d5db;
  color: #374151;
  border: 1px solid transparent;
  border-radius: 0.25rem;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
`

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
      <ControlContainer >
        <p className='paragraph'>
          <Label className={`label ${emailNotValid ? 'invalid' : ''}`}>
            Email
          </Label>
          <Input
            type="email"
            //style={{
              //backgroundColor: emailNotValid ? '#fed2d2' : '#d1d5db'
            //}}
            className={emailNotValid ? 'invalid' : undefined}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        </p>
        <p>
          <Label className={`label ${emailNotValid ? 'invalid' : ''}`}>
            Password
          </Label>
          <Input
            type="password"
            className={passwordNotValid ? 'invalid' : undefined}
            onChange={(event) =>
              handleInputChange('password', event.target.value)
            }
          />
        </p>
      </ControlContainer>
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
<summary>Dynamic & Conditional Styling with Styled Components</summary>

In this section we still discuss about AuthInputs.jsx file especially in a Label. We can eliminate the the code components into a clean code like this :

```javascript
<Label invalid={emailNotValid}>Email</Label>
```

Note : the name invalid is free. You can use another name.

So now we should modify the code on const Label especially in color. Make a change on css code by creating an arrow function like You see below :

```javascript
const Label = styled.label`
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: ${({invalid}) => invalid ? '#f87171' :'#6b7280'} ;
`;
```

Also we can modify on const Input :

```javascript
<Input
  invalid={emailNotValid}
  type="email"
  //style={{
  //backgroundColor: emailNotValid ? '#fed2d2' : '#d1d5db'
  //}}
  className={emailNotValid ? 'invalid' : undefined}
  onChange={(event) => handleInputChange('email', event.target.value)}
/>
```

In cosnt Input we can modify into :

```javascript
const Input = styled.input`
  width: 100%;
  padding: 0.75rem 1rem;
  line-height: 1.5;
  background-color: ${({invalid}) => invalid ? '#fed2d2' : '#d1d5db'};
  color: ${({invalid}) => invalid ? '#ef4444' : '#374151'};
  border: 1px solid ${({invalid}) => invalid ? '#f73f3f' : 'transparent'} ;
  border-radius: 0.25rem;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
`;
```

Note : The data codes above is taken from index.css data. We can see below 

```css
input.invalid {
  color: #ef4444;
  border-color: #f73f3f;
  background-color: #fed2d2;
}
```

Also here we can modify again on a Label and the Input Password 

Update the code into :

```javascript
<Label invalid={passwordNotValid}>Password</Label>
  <Input
  invalid={passwordNotValid}
  type="password"
  className={passwordNotValid ? 'invalid' : undefined}
  onChange={(event) =>
  handleInputChange('password', event.target.value)
  }
  />
```

And also in javascript, This is a valid rule when we change the **invalid** code into **$invalid**. Using a dollar $ sign.

And here is the complete code of AuthInputs.jsx file after we modified :

```javascript
import { useState } from 'react';
import { styled } from 'styled-components';

const ControlContainer = styled.div`
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
`;

const Label = styled.label`
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: ${({$invalid}) => $invalid ? '#f87171' :'#6b7280'} ;
`;

const Input = styled.input`
  width: 100%;
  padding: 0.75rem 1rem;
  line-height: 1.5;
  background-color: ${({$invalid}) => $invalid ? '#fed2d2' : '#d1d5db'};
  color: ${({$invalid}) => $invalid ? '#ef4444' : '#374151'};
  border: 1px solid ${({$invalid}) => $invalid ? '#f73f3f' : 'transparent'} ;
  border-radius: 0.25rem;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
`;

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
      <ControlContainer >
        <p className='paragraph'>
          <Label $invalid={emailNotValid}>Email</Label>
          <Input
            $invalid={emailNotValid}
            type="email"
            //style={{
              //backgroundColor: emailNotValid ? '#fed2d2' : '#d1d5db'
            //}}
            className={emailNotValid ? 'invalid' : undefined}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        </p>
        <p>
          <Label $invalid={passwordNotValid}>Password</Label>
          <Input
            $invalid={passwordNotValid}
            type="password"
            className={passwordNotValid ? 'invalid' : undefined}
            onChange={(event) =>
              handleInputChange('password', event.target.value)
            }
          />
        </p>
      </ControlContainer>
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
<summary>Styled Components : Pseudo Selectors, Nested Rules & Media Queries</summary>

In this case we can modify the code from Header.jsx file and make a custom constant Header

So that we can copy & paste the code from Header.module.css in header section like this :

```css
header {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 2rem;
  margin-bottom: 2rem;
}
```

So paste the code in Header.jsx file after const SytledHeader and then change the <header into <StyledHeader as edited below :

```javascript
import { styled } from 'styled-components';

import logo from '../assets/logo.png';
import classes from './Header.module.css';

const StyledHeader = styled.header`
display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 2rem;
  margin-bottom: 2rem;
`;

export default function Header() {
  return (
    <StyledHeader>
      <img src={logo} alt="A canvas" />
      <h1>ReactArt</h1>
      <p className={classes.paragraph}>A community of artists and art-lovers.</p>
    </StyledHeader>
  );
}

```

Or in another case we can paste all css codes from Header.module.css into Header.jsx file and replace the **header** into a sign **&**. You can see below :

```javascript
import { styled } from 'styled-components';

import logo from '../assets/logo.png';
import classes from './Header.module.css';

const StyledHeader = styled.header`
display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 2rem;
  margin-bottom: 2rem;

  & img {
  object-fit: contain;
  margin-bottom: 2rem;
  width: 11rem;
  height: 11rem;
  }

  & h1 {
  font-size: 1.5rem;
  font-weight: 600;
  letter-spacing: 0.4em;
  text-align: center;
  text-transform: uppercase;
  color: #9a3412;
  font-family: 'Pacifico', cursive;
  margin: 0;
  }

  & p {
  text-align: center;
  color: #a39191;
  /* color : red; */
  margin: 0;
  }

  @media (min-width: 768px) {
  
  margin-bottom: 4rem;

  & h1 {
    font-size: 2.25rem;
  }
}
`;

export default function Header() {
  return (
    <StyledHeader>
      <img src={logo} alt="A canvas" />
      <h1>ReactArt</h1>
      <p className={classes.paragraph}>A community of artists and art-lovers.</p>
    </StyledHeader>
  );
}

```

While css codes from Header.module.css we can see before it be pasted into Header.jsx file :

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

.paragraph {
  text-align: center;
  color: #a39191;
  /* color : red; */
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

And here we can also modify the css code from index.css into AuthInputs.jsx file and make a constant variable for example **const Button** = **style.button**

And ofcourse we can copy and paste the button css code in index.css and also we can add it's hover styling. And don't foget to replace **button** into **&** sign. And replace <button into <Button

```css
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
```

Here is the modified codes of AuthInputs.jsx

Note : we can eliminate also the className=? in <Button

```javascript
import { useState } from 'react';
import { styled } from 'styled-components';

const ControlContainer = styled.div`
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
`;

const Label = styled.label`
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: ${({$invalid}) => $invalid ? '#f87171' :'#6b7280'} ;
`;

const Input = styled.input`
  width: 100%;
  padding: 0.75rem 1rem;
  line-height: 1.5;
  background-color: ${({$invalid}) => $invalid ? '#fed2d2' : '#d1d5db'};
  color: ${({$invalid}) => $invalid ? '#ef4444' : '#374151'};
  border: 1px solid ${({$invalid}) => $invalid ? '#f73f3f' : 'transparent'} ;
  border-radius: 0.25rem;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
`;

const Button = styled.button`
  padding: 1rem 2rem;
  font-weight: 600;
  text-transform: uppercase;
  border-radius: 0.25rem;
  color: #1f2937;
  background-color: #f0b322;
  border-radius: 6px;
  border: none;

  &:hover {
    background-color: #f0920e;
  }
`;

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
      <ControlContainer >
        <p className='paragraph'>
          <Label $invalid={emailNotValid}>Email</Label>
          <Input
            $invalid={emailNotValid}
            type="email"
            //style={{
              //backgroundColor: emailNotValid ? '#fed2d2' : '#d1d5db'
            //}}
            className={emailNotValid ? 'invalid' : undefined}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        </p>
        <p>
          <Label $invalid={passwordNotValid}>Password</Label>
          <Input
            $invalid={passwordNotValid}
            type="password"
            className={passwordNotValid ? 'invalid' : undefined}
            onChange={(event) =>
              handleInputChange('password', event.target.value)
            }
          />
        </p>
      </ControlContainer>
      <div className="actions">
        <button type="button" className="text-button">
          Create a new account
        </button>
        <Button onClick={handleLogin}>
          Sign In
        </Button>
      </div>
    </div>
  );
}

```

In the end, we check into web and we'll see the button **SIGN IN** is styled hover.

</details>

<details>
<summary>Creating Reusable Components & Component Combinations</summary>

If we see in AuthInputs.jsx file, there so many css codes. To solve this we should create a new separate file. Here for example we create Button.jsx, Input.jsx and Label.jsx files for a separate css. We put it in **components** folder.

First in a Button.jsx file we paste the css codes from AuthInputs.jsx file. also import the styled and export it.

== Button.jsx ==

```javascript
import { styled } from 'styled-components';

const Button = styled.button`
  padding: 1rem 2rem;
  font-weight: 600;
  text-transform: uppercase;
  border-radius: 0.25rem;
  color: #1f2937;
  background-color: #f0b322;
  border-radius: 6px;
  border: none;

  &:hover {
    background-color: #f0920e;
  }
`;

export default Button;
```

And don't forget to put the import code in AuthInputs.jsx file for the Button.jsx file

== AuthInputs.jsx == for the import Button.jsx file

```javascript
import Button from './Button.jsx';
```

We could do the same on a Input.jsx file. We can cut & paste the const Label and Input into Input.jsx file from AuthInput.jsx file. Also import the styled, but here we can create an export function. We name it e.g function CustomInput() that returns the paragraph and also adding the props e.g `{label, ...props}`

=== Input.jsx ===

```javascript
import { styled } from 'styled-components';

const Label = styled.label`
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: ${({$invalid}) => $invalid ? '#f87171' :'#6b7280'} ;
`;

const Input = styled.input`
  width: 100%;
  padding: 0.75rem 1rem;
  line-height: 1.5;
  background-color: ${({$invalid}) => $invalid ? '#fed2d2' : '#d1d5db'};
  color: ${({$invalid}) => $invalid ? '#ef4444' : '#374151'};
  border: 1px solid ${({$invalid}) => $invalid ? '#f73f3f' : 'transparent'} ;
  border-radius: 0.25rem;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
`;

export default function CustomInput({label, invalid, ...props}) {
    return <p>
        <Label $invalid = {invalid}>{label}</Label>
        <Input $invalid = {invalid} {...props} />
    </p>
}
```

Also we put the import Input.jsx into AuthInputs.jsx

```javascript
import Input from './Input.jsx';
```

And we can delete some codes from AuthInput.jsx file

```javascript
<p className='paragraph'>
<Label $invalid={emailNotValid}>Email</Label>
</p>

<p>
<Label $invalid={passwordNotValid}>Password</Label>
</p>
```

And change (update) to props codes below in AUthInput.jsx file 

```javascript
<Input
  label="Email"
  invalid={emailNotValid}
  type="email"
  //style={{
  //backgroundColor: emailNotValid ? '#fed2d2' : '#d1d5db'
  //}}
  className={emailNotValid ? 'invalid' : undefined}
  onChange={(event) => handleInputChange('email', event.target.value)}
/>
        
<Input
  invalid={passwordNotValid}
  label="Password"
  type="password"
  className={passwordNotValid ? 'invalid' : undefined}
  onChange={(event) =>
  handleInputChange('password', event.target.value)
}
/>
```
When we visi the website of http://localhost:5173/ , The details of the input and labels are still the same.

And here is the complete codes of AuthInputs.jsx after modified :

```javascript
import { useState } from 'react';
import { styled } from 'styled-components';

import Button from './Button.jsx';
import Input from './Input.jsx';

const ControlContainer = styled.div`
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
`;

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
      <ControlContainer >
          <Input
            label="Email"
            invalid={emailNotValid}
            type="email"
            //style={{
              //backgroundColor: emailNotValid ? '#fed2d2' : '#d1d5db'
            //}}
            className={emailNotValid ? 'invalid' : undefined}
            onChange={(event) => handleInputChange('email', event.target.value)}
          />
        
          <Input
            invalid={passwordNotValid}
            label="Password"
            type="password"
            className={passwordNotValid ? 'invalid' : undefined}
            onChange={(event) =>
              handleInputChange('password', event.target.value)
            }
          />
      </ControlContainer>
      <div className="actions">
        <button type="button" className="text-button">
          Create a new account
        </button>
        <Button onClick={handleLogin}>
          Sign In
        </Button>
      </div>
    </div>
  );
}

```

**Styled Components : Advantages & Disadvantages**

== Advantages ==

- Quick & Easy to add
- You continue "thinking in React" --> configurable style functions
- Styles are scoped to components --> No CSS rules clashes

== Disadvantages ==

- You need to know CSS
- No clear separation of React & CSS Code
- You end up with many relatively small wrapper components

</details>

<details>
<summary>Introducing Talwind CSS For React App Styling</summary>

We can visit this website --> https://tailwindcss.com/docs/installation/using-vite

**Installation**

Get started with Tailwind CSS

Tailwind CSS works by scanning all of your HTML files, JavaScript components, and any other templates for class names, generating the corresponding styles and then writing them to a static CSS file.

It's fast, flexible, and reliable — with zero-runtime.

Intallation Using Vite :

Installing Tailwind CSS as a Vite plugin is the most seamless way to integrate it with frameworks like Laravel, SvelteKit, React Router, Nuxt, and SolidJS.

**Create your project**

Start by creating a new Vite project if you don’t have one set up already. The most common approach is to use Create Vite.

```javascript
npm create vite@latest my-project
cd my-project
```

**Install Tailwind CSS**

Install tailwindcss and @tailwindcss/vite via npm.

```javascript
npm install tailwindcss @tailwindcss/vite
```

**Configure the Vite plugin**

Add the @tailwindcss/vite plugin to your Vite configuration.

```javascript
import { defineConfig } from 'vite'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [
    tailwindcss(),
  ],
})
```

**Import Tailwind CSS**

Add an @import to your CSS file that imports Tailwind CSS.

```javascript
@import "tailwindcss";
```

**Start your build process**

Run your build process with npm run dev or whatever command is configured in your package.json file.

```javascript
npm run dev
```

**Start using Tailwind in your HTML**

Make sure your compiled CSS is included in the <head> (your framework might handle this for you), then start using Tailwind’s utility classes to style your content.

```javascript
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="/src/style.css" rel="stylesheet">
</head>
<body>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</body>
</html>
```

It's time to practice, first we can run a command :

We can directly install the Tailwindcss, 

Note : If the vite is outdated we can re-install again such this commands :

```md
npm install vite@latest
```

we can immediately install the tailwind. There are to ways to install it by using command 

```css
npm install tailwindcss @tailwindcss/vite
```

Or

```css
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

But the first way is recomended

We try to install it now :

```css
user@aziz MINGW64 /d/course/udemy/react/Section6/01-starting-project
$ npm install tailwindcss @tailwindcss/vite

added 20 packages, and audited 280 packages in 4s

120 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

```

Note : If we still use the old command like *npm install -D tailwindcss postcss autoprefixer* and *npx tailwindcss init -p*. After we did it, we could find the two new files on our project. Usually the name is postcss.confi.js and tailwind.config.css

Because We're using the newest way to install the tailwind, then to configure it we can paste the code on vite.config.js file and import this codes *import tailwindcss from '@tailwindcss/vite'* also put the tailwindcss(), after the plugin code

== vite.config.js ==

```javascript
import { defineConfig } from 'vite'
import tailwindcss from '@tailwindcss/vite'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    tailwindcss(),
  ],
})

```

Next, we can add an import on our css file

== index.css ===

```css
@import "tailwindcss";

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

Run the command **npm run dev** and the result is still the same 

Note : But before we should install **Tailwind CSS IntelliSense** on our Visual Studio code in our project.

</details>

<details>
<summary>Tailwind 3 Vs 4</summary>

Tailwind 3 vs 4
The next lecture were recorded with Tailwind v3 being used.

To follow along smoothly, it's therefore recommended to also use that version. You find the setup documentation (which I also show in the next lectures) here: https://v3.tailwindcss.com/docs/installation.

Important: To install v3, use the below command (besides that, follow the instructions from the above link):

```md
npm install -D tailwindcss@3 postcss autoprefixer
npx tailwindcss@3 init -p 
(the @3 is important!)
```

Please note: This has nothing to do with the React version being used! All the code works with the latest React version.
</details>

<details>
<summary>Adding & Using Tailwind CSS In A React Project</summary>

This section is actually different in tutorial video. Because it's old one.

But We use the newest step for tailwind installation. So that has been explained in previous Section before this section.
</details>
