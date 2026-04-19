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
