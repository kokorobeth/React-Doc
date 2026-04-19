<details>
  <summary>Module Introduction & A Challenge For You!</summary>

  **React Essentials - Practice Project**
  *Apply your knowledge & Practice What You learned*

  - Build an *Investment Calculator* Web App
  - Build, Configure, & Combine *Components*
  - Manage Application *State*
  - Output *List* & *Conditional* Content

  **Your Task**
  *Build an Investment Calculator web app*

  Use the starting project attached to this lecture

  Add components for displaying a header, fecthing user input & outputing the results table

  Fetch & store user input ie. the entered investment parameters

  Derive Investment results with help of the provided utility function in the starting project

  Display investment result in a HTML table ie 
  
  ```md
  use<table>, <thead>, <tbody>, <tr>, <th>, <td>
  ```

  Conditionally display an info message if an invalid duration (<1) was entered

  Let's start the project by using this command to install the project

  ```md
  npm install
  ```

  The files are provided, and we can try to npm run dev command. Inside the folders we provide **util** folder, inside of that folder there's a file named investment.js and an image in **assets** folder named investment-calculator.png. 

  *investment.js* file :

  ```javascript
  // This function expects a JS object as an argument
// The object should contain the following properties
// - initialInvestment: The initial investment amount
// - annualInvestment: The amount invested every year
// - expectedReturn: The expected (annual) rate of return
// - duration: The investment duration (time frame)
export function calculateInvestmentResults({
  initialInvestment,
  annualInvestment,
  expectedReturn,
  duration,
}) {
  const annualData = [];
  let investmentValue = initialInvestment;

  for (let i = 0; i < duration; i++) {
    const interestEarnedInYear = investmentValue * (expectedReturn / 100);
    investmentValue += interestEarnedInYear + annualInvestment;
    annualData.push({
      year: i + 1, // year identifier
      interest: interestEarnedInYear, // the amount of interest earned in this year
      valueEndOfYear: investmentValue, // investment value at end of year
      annualInvestment: annualInvestment, // investment added in this year
    });
  }

  return annualData;
}

// The browser-provided Intl API is used to prepare a formatter object
// This object offers a "format()" method that can be used to format numbers as currency
// Example Usage: formatter.format(1000) => yields "$1,000"
export const formatter = new Intl.NumberFormat('en-US', {
  style: 'currency',
  currency: 'USD',
  minimumFractionDigits: 0,
  maximumFractionDigits: 0,
});

  ```
  
</details>

<details>
<summary>Adding a Header Component</summary>

First, we create **components** folder in src folder and create a file *Header.jsx* 

```javascript
import logo from '../assets/investment-calculator-logo.png';

export default function Header() {
    return (
        <header id='header'>
            <img src={logo} alt="Logo showing a money bag" />
            <h1>Investment Calculator</h1>
        </header>
    )
}
```

As we see here on App.jsx file, we can modify the codes and import the file of Header.jsx

```javascript
import Header from "./components/Header.jsx";

function App() {
  return (
    <Header />
  )
}

export default App

```

On index.html file we can add an id="root" 

```javascript
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/investment-calculator-logo.png" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React Investment Calculator</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/index.jsx"></script>
  </body>
</html>

```

also adding an id="header" on Header.jsx file that comes from index.css file

```css
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@400;700&family=Roboto+Condensed:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: 'Quicksand', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: radial-gradient(#303b37, #1a1f1d);
  color: #e1eeeb;
  min-height: 100vh;
}

#header {
  text-align: center;
  margin: 3rem auto;
}


#header img {
  width: 5rem;
  height: 5rem;
  object-fit: contain;
  background-color: transparent;
}

#header h1 {
  font-size: 1.5rem;
}

#user-input {
  padding: 1rem;
  max-width: 30rem;
  margin: 2rem auto;
  border-radius: 4px;
  background: linear-gradient(180deg, #307e6c, #2b996d);
}

.input-group {
  display: flex;
  justify-content: space-evenly;
  gap: 1.5rem;
}

#user-input label {
  display: block;
  margin-bottom: 0.25rem;
  font-family: 'Roboto Condensed', sans-serif;
  font-size: 0.5rem;
  font-weight: bold;
  text-transform: uppercase;
}

#user-input input {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #76c0ae;
  border-radius: 0.25rem;
  background-color: transparent;
  color: #c2e9e0;
  font-size: 1rem;
}

#result {
  max-width: 50rem;
  margin: 2rem auto;
  padding: 1rem;
  table-layout: fixed;
  border-spacing: 1rem;
  text-align: right;
}

#result thead {
  font-size: 0.7rem;
  color: #83e6c0;
}

#result tbody {
  font-family: 'Roboto Condensed', sans-serif;
  font-size: 0.85rem;
  color: #c2e9e0;
}

.center {
  text-align: center;
}
```

</details>

<details>
<summary>Getting Started with a User Input Component</summary>

In this section we can add again a new component as UserInput.jsx in a component folder

```javascript
export default function UserInput() {
    return <section id="user-input">
        <div className="input-group">
            <p>
                <label>Initial Investment</label>
                <input type="number" required />
            </p>
            <p>
                <label>Annual Investment</label>
                <input type="number" required />
            </p>
        </div>
        <div className="input-group">
            <p>
                <label>Expected Return</label>
                <input type="number" required />
            </p>
            <p>
                <label>Duration</label>
                <input type="number" required />
            </p>
        </div>
    </section>
}
```
</details>
