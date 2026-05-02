<details>
<summary>Module Introduction</summary>

**Finding & Fixing Errors**

- Making sense of *React Error Messages*
- Finding *Logical errors* via the Browser *DevTools & Debugger*
- Enabling Reacts *Strict Mode*
- Using the *React DevTools* for Application Analysis & Manipulation

</details>

<details>
<summary>The Starting Project</summary>

In this lesson we would like to use the previous material in **Investment Calculator** as we learned before. 

</details>

<details>
<summary>Understanding React Error Messages</summary>

In this lesson we would like to use the previous material in **Investment Calculator** as we learned before. 

The source codes link is here :

https://github.com/academind/react-complete-guide-course-resources/blob/main/attachments/06%20Debugging/01-starting-project.zip

If we inspect the element there would be some error on there when we put some negative values or put zero value. 

And the first step here is to add if check on Results.jsx file

```javascript
  if (results.length) {
    return <p className='center'>Invalid input data provided.</p>
  }
```

To make sure that the *const initialInvestment* could not be executed

Here is the complete code of Results.jsx file 

```javascript
import { calculateInvestmentResults, formatter } from '../util/investment.js';


export default function Results({ input }) {
  const results = [];
  calculateInvestmentResults(input, results);

  if (results.length) {
    return <p className='center'>Invalid input data provided.</p>
  }

  const initialInvestment =
    results[0].valueEndOfYear -
    results[0].interest -
    results[0].annualInvestment;

  return (
    <table id="result">
      <thead>
        <tr>
          <th>Year</th>
          <th>Investment Value</th>
          <th>Interest (Year)</th>
          <th>Total Interest</th>
          <th>Invested Capital</th>
        </tr>
      </thead>
      <tbody>
        {results.map((yearData) => {
          const totalInterest =
            yearData.valueEndOfYear -
            yearData.annualInvestment * yearData.year -
            initialInvestment;
          const totalAmountInvested = yearData.valueEndOfYear - totalInterest;

          return (
            <tr key={yearData.year}>
              <td>{yearData.year}</td>
              <td>{formatter.format(yearData.valueEndOfYear)}</td>
              <td>{formatter.format(yearData.interest)}</td>
              <td>{formatter.format(totalInterest)}</td>
              <td>{formatter.format(totalAmountInvested)}</td>
            </tr>
          );
        })}
      </tbody>
    </table>
  );
}

```

So when we check the browser after *npm run dev*, there is nor crash error again when we input the zero value or negative values.

</details>

<details>
<summary>Using the Browser Debugger & Breakpoints</summary>

In this case we only explore about the codes on inpections area, after we inspect them. We would see the codes on the browser. And jump to the Sources section.

Note : Analyze and solve it!

</details>

<details>
<summary>Understanding React's Strict Mode</summary>

In this section. There's a changes on Results.jsx file like we show below here :

```javascript
import { calculateInvestmentResults, formatter } from '../util/investment.js';


export default function Results({ input }) {
  const results = [];
  calculateInvestmentResults(input, results);

  if (results.length === 0) {
    return <p className="center">Invalid input data provided.</p>
  }

  const initialInvestment =
    results[0].valueEndOfYear -
    results[0].interest -
    results[0].annualInvestment;

  return (
    <table id="result">
      <thead>
        <tr>
          <th>Year</th>
          <th>Investment Value</th>
          <th>Interest (Year)</th>
          <th>Total Interest</th>
          <th>Invested Capital</th>
        </tr>
      </thead>
      <tbody>
        {results.map((yearData) => {
          const totalInterest =
            yearData.valueEndOfYear -
            yearData.annualInvestment * yearData.year -
            initialInvestment;
          const totalAmountInvested = yearData.valueEndOfYear - totalInterest;

          return (
            <tr key={yearData.year}>
              <td>{yearData.year}</td>
              <td>{formatter.format(yearData.valueEndOfYear)}</td>
              <td>{formatter.format(yearData.interest)}</td>
              <td>{formatter.format(totalInterest)}</td>
              <td>{formatter.format(totalAmountInvested)}</td>
            </tr>
          );
        })}
      </tbody>
    </table>
  );
}
```

Source link : https://github.com/academind/react-complete-guide-course-resources/blob/main/attachments/06%20Debugging/Results.jsx

But when we see on the browser, it seems to be longer result on there. 

Using strict mode typically start from index.jsx file

And we can wrap the <App component by using <StrictMode

And it can catch some certain problem in our apps.

As we see below :

```javascript
import { StrictMode } from 'react';
import ReactDOM from 'react-dom/client';

import App from './App.jsx';
import './index.css';

ReactDOM.createRoot(document.getElementById('root')).render(
    <StrictMode>
        <App />
    </StrictMode>
);

```
</details>

<details>
<summary>Using the React DevTools (Browser Extension)</summary>

In this section we would like to install react devtools. Here we can search on the google browser for **react devtools**

CLicking it and add to chrome 

Here is the link : https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en

After we add to chrome, we inspect it we could see two elements shown on that.

Profiler and Components

<img width="133" height="222" alt="image" src="https://github.com/user-attachments/assets/1e151685-6e4f-40f9-afd3-6911c03eb56b" />


</details>
