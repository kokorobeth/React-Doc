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

</details>


