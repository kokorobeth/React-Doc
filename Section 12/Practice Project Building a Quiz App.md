<details>
<summary>Module Introduction & Starting Project</summary>

In this course section, we'll dive into a brand new demo project and we're going to build this project from scratch, from the ground up.

And whilst building this project, we will continue working with side effects and the useEffect hook. And therefore, the idea behind this course section here is to give you an opportunity to practice what you learned and to dive a bit deeper into React and effects.

Therefore, in this section, you can apply your existing React and effects knowledge. We'll continue dealing with effect dependencies and cleanup functions, so that you get a better feeling for when to add and use those things.

And since we're going to build a brand new project from the ground up, you will also see how you can combine effects with other React concepts.

And therefore, in this section you can absolutely try building this project on your own as a practice. But the main idea indeed is that we'll build it together step by step, that I explain why we build it like this and that therefore, whilst you are following along and you're also building it on your own, whilst watching those videos, you get a better understanding of all these crucial concepts.

Now, as always, for this section here, I prepared a starting project, a local and a CodeSandbox version.

In the local version, as always, you need to run npm install and npm run dev. In the CodeSandbox version, you don't need to do that.

And once you got this project started up, you should see a screen like this, if you visit the running development server.

So not a lot on it, because that's what we're going to build together throughout this section.

Because as mentioned, we're going to build this project from scratch. And we're therefore going to use effects again, because we'll need them for this project.

But we'll also revisit Components and all those things.
</details>

<details>
<summary>A First Component & Some State</summary>

So let's get started with building this quiz project.

And I will get started by adding a couple of components. Therefore, as a first step, I'll add this Components folder in the src folder.

And in there I want to add a Header.jsx file to hold the header, which I want to show on top of my page. And I'll add a Quiz.jsx file because as you saw before in this section, we're going to build a quiz web app.

And therefore I'll add such a Quiz component which will control this quiz and render other quiz-related components.

But I'll start with the header. In there I'll add my Header function component, and of course also export it, as you learned it before in this course, and as we did it many times before in this course.

And then here I wanna return the built-in header element which should be wrapped around an img element and an h1 element.

Now, in the h1 element, which should display my main title on the page, I'll output ReactQuiz.

And for the image, it's this quiz-logo.png file, which I wanna display.

And here's one important note, by the way. Definitely feel free to pause these videos at any point of time throughout this section to try out the next steps on your own.

So if I'm, for example, saying that I want to display an image here and I tell you which image, you can pause the video and add the code for that on your own.

And the same is true for when I start adding new components or I start managing some state and so on. Whenever I tell you that I'm about to do something, definitely consider pausing the video and trying it on your own because that will be a great exercise and practice.

So, here, to display this quiz-logo.png file, I'll go back to the Header.jsx file and import this logo image from...

And then going up one level here, actually, since I'm in the Components folder, then I'll dive into the assets folder, and then there it's this quiz-logo.png file, which I wanna target.

And with that import added, you learned before that in most React projects, this Vite-based project included, I can set the source of the image to this imported image here, and the project setup will then figure out and inject the path to the, potentially, optimized image behind the scenes.

Now we also want to add an alt text here. And here, I'll just say quiz logo. You could of course be a bit more descriptive here.

With that, we got a very basic component, no effects, no state, because not all components need that. Indeed, most components don't need state or don't need effects.

**Header.jsx** component file :

```javascript
import logoImg from '../assets/quiz-logo.png';

export default function Header() {
    return (
        <header>
            <img src={logoImg} alt='Quiz Logo' />
            <h1>ReactQuiz</h1>
        </header>
    )
}
```

And therefore, now that we added this Header component, we can go to the App component file, the App.jsx file, and import Header from ./components/Header.jsx like this.

**App.jsx** component file :

```javascript
import Header from "./components/Header.jsx";

function App() {
    return (
        <Header />
    )
}

export default App;

```

And then simply return this custom Header component here.

And if you save everything, you should therefore then see this header here on the page.

![alt text](image.png)

And that's of course a great first step, but of course, also pretty basic.

Therefore, we'll continue right away and also start working on the Quiz component.

Now my idea behind this component is that in there I want to show the currently active question to the user.

And when the question was answered by the user, I wanna switch to a different question.

So it should be this Quiz component that's responsible for switching between questions and registering user answers.

But of course, I'll simply start by exporting a new component function, which is called Quiz.

And then in this component, as mentioned, I wanna output the question, so the currently active question.

And this, of course, will soon be replaced with more meaningful content. That's the idea.

And then, as mentioned, in this component I wanna manage what the currently active question is, and I want to change to a different question whenever the user answers a question, and I want to store those answers.

Therefore, we'll definitely need to manage some state here, which we do with the useState hook imported from React because we need to register those answers, for example.

So, therefore, here we could add two pieces of state.

The first piece of state is the currently active question.

And for that, let's simply assume that we get an array of questions. I will soon provide you with some dummy data which will be such an array.

And therefore the currently active question could simply be managed through the index of the currently active question.

If we got an array of questions, we could simply manage the index of the currently displayed question here and change that index whenever the user answered a question.

So here we could then have the activeQuestionIndex and a setActiveQuestionIndex updating function.

That would be one way of managing which question should be displayed to the user.

And then, I'll also add a second piece of state here where I wanna register the answers selected by the user because every question will come with multiple possible answers.

And, of course, throughout the quiz, I wanna store all the answers picked by the user.

And therefore, we'll, well, need some state where we do store those answers.

And that could also be an array where we basically just add answer by answer to this array.

And I'll name this state here userAnswers and setUserAnswers because these are the answers picked by the user.

But I can already tell you that this would be a possible way of managing the state, but in my opinion, not necessarily the best way.

**Quiz.jsx** component file :

```javascript
import { useState } from 'react';

export default function Quiz() {
    const [activeQuestionIndex, setActiveQuestionIndex] = useState(0);
    const [userAnswers, setUserAnswers] = useState([]);

    return (
        <p>Currently active Question</p>
    )
}
```
</details>

<details>
<summary>Deriving Values, Outputting Questions & Registering Answers</summary>

So we got started adding some components and we got started managing some state here in the Quiz component.

Now a lot of logic is missing and of course the questions are missing. And before we'll improve the logic, I will indeed give you some questions here, so that we do have some questions to work with.

Therefore, attached to this lecture, you find a questions.js file, which you should add to your project right next to the main.jsx file.

**question.js**
```javascript
export default [
  {
    id: 'q1',
    text: 'Which of the following definitions best describes React.js?',
    answers: [
      'A library to build user interfaces with help of declarative code.',
      'A library for managing state in web applications.',
      'A framework to build user interfaces with help of imperative code.',
      'A library used for building mobile applications only.',
    ],
  },
  {
    id: 'q2',
    text: 'What purpose do React hooks serve?',
    answers: [
      'Enabling the use of state and other React features in functional components.',
      'Creating responsive layouts in React applications.',
      'Handling errors within the application.',
      'Part of the Redux library for managing global state.',
    ],
  },
  {
    id: 'q3',
    text: 'Can you identify what JSX is?',
    answers: [
      'A JavaScript extension that adds HTML-like syntax to JavaScript.',
      'A JavaScript library for building dynamic user interfaces.',
      'A specific HTML version that was explicitly created for React.',
      'A tool for making HTTP requests in a React application.',
    ],
  },
  {
    id: 'q4',
    text: 'What is the most common way to create a component in React?',
    answers: [
      'By defining a JavaScript function that returns a renderable value.',
      'By defining a custom HTML tag in JavaScript.',
      'By creating a file with a .jsx extension.',
      'By using the "new" keyword followed by the component name.',
    ],
  },
  {
    id: 'q5',
    text: 'What does the term "React state" imply?',
    answers: [
      'An object in a component that holds values and may cause the component to render on change.',
      'The lifecycle phase a React component is in.',
      'The overall status of a React application, including all props and components.',
      'A library for managing global state in React applications.',
    ],
  },
  {
    id: 'q6',
    text: 'How do you typically render list content in React apps?',
    answers: [
      'By using the map() method to iterate over an array of data and returning JSX.',
      'By using the for() loop to iterate over an array of data and returning JSX.',
      'By using the forEach() method to iterate over an array of data and returning JSX.',
      'By using the loop() method to iterate over an array of data and returning JSX.',
    ],
  },
  {
    id: 'q7',
    text: 'Which approach can NOT be used to render content conditionally?',
    answers: [
      'Using a the #if template syntax.',
      'Using a ternary operator.',
      'Using the && operator.',
      'Using an if-else statement.',
    ],
  },
];
```

So simply grab that attached file, insert it next to the main.jsx file. And in that questions.js file, you'll find an array that's being exported, which is full of dummy questions with possible answers for all those questions.

And you'll see that every question has an ID, a text, and then those mentioned answers.

And what's important about those answers is that it's always the first answer that's correct.

Now of course, when we display those answers to the user, we therefore want to shuffle them so that there it's not always the first answer that's correct.

But here in the raw data, it is the first answer so that in our web app logic, we can determine whether the user picked the right answer or not.

But we'll work on that logic a little bit later.

But now that we got this array of questions here, let's come back to this quiz state.

Why is this way of managing the state not optimal, in my opinion?

What could be the reason for that? What could be wrong here?

Well, at the moment, I plan to have two state snapshots here: the index of the currently active question and then an array of answers selected by the user.

Now, if you take a closer look at this implementation, you might see that in the end, one of the two pieces of state here is redundant because, of course, we will definitely need to store the answers picked by a user.

But when it comes to the active question index, that could actually be derived from this userAnswers array here.

Because here we will store one answer for every question. And therefore, we can simply take a look at the number of stored answers in this array, and we can derive what the currently active question index should be.

Because of course, if we have like two answers in that array, it's the third question we now want to present to the user because the first two questions have then already been answered.

Therefore, we can get rid of this activeQuestionIndex state and instead add some derived state, a computed value to this component here.

The active question index can simply be a const where we take the userAnswers and then the length of this array.

And therefore, if this is an empty array, this will give us zero and the active question index will be zero.

So it will then be the first question which we want to show to the user.

If one answer has been added because the first question has been answered, this index here will be one and therefore the second question in this questions array.

And that's therefore a better way of managing the state because when working with React, when writing React code, you typically want to manage as little state as possible and derive as much state as possible instead.

And that's what we're doing here.

And therefore, with this change here, which optimizes our code, we can now finally work on presenting a question to the user.

And therefore we want to, of course, import this questions array and then output the text of the question with the currently active question index on the screen.

Therefore, here in this component, in the Quiz component, we can import our dummy questions, maybe named like this to make it clear that this is some dummy raw data we're importing from going up one level, and then there is the questions.js file.

And then here, instead of outputting this paragraph, we can output an h2 tag, let's say, where we then output questions, access the activeQuestionIndex, and then the text property because that's the question text that should be displayed.

And of course, we also want to output the possible answers below that.

So therefore, we can actually wrap this into a div with an ID of question for styling purposes here because in this starting project I gave you, in the index.css file, I already set up a bunch of styles.

And therefore, if you use the ID question on this div, we should get some nicer styling.

And below this h2 tag, we output an unordered list, which should get an ID of answers, also for styling purposes.

And here, we then want to dynamically output all those possible answers.

Now, I said before that they should be shuffled and we will soon do that, but for the moment, just to see something on the screen, I'll simply access my question for the currently active question index, then the answers, and then we can map this list of answers, so this list of strings, to a list of JSX components as you learned early in this course.

Here, we'll get the answer in this function, and for every answer, I want to output a list item where every list item will get a key, which here could be the answer itself because the answer is just a string, but it will be a different string, a different text for every answer.

So this is indeed a unique identifier we can use.

And I'll also give every list item a className of answer, again, for styling purposes.

And then between those li tags, I want to output a button because those answers, of course, should be clickable, they should be selectable, and therefore, for semantic reasons, I'm outputting a button element.

And then here, between my button tags, I want to output the answer, so this answer text that should be displayed.

And with that, we're outputting those questions.

We can then actually also already add a function that we could call handleSelectAnswer, so that should be triggered when this button here is pressed.

And therefore, on this button, we should add the onClick prop and point at handleSelectAnswer, so that this function will be triggered.

And then in there, I want to store the selected answer in my userAnswers array.

Now therefore, of course, I'll need to get the selected answer here as a value, as a parameter, so that in here we can then update the userAnswers state.

And therefore, in order to make sure that the selected answer reaches this function, it's, of course, not enough to just point at handleSelectAnswer like this down there.

Because like this, React would just call this for us, and React, of course, would not know that it should pass the selected answer along.

And therefore, we'll instead wrap this with an arrow function here in this case, so wrap it with some other function, which will then be the function invoked by React.

So that in this potentially invoked function, we have more control over how handleSelectAnswer will be invoked, and we can now pass the answer we got here to handleSelectAnswer.

And this will still not be executed immediately when this code here is parsed, but instead still only when the button is clicked because it's then this outer function that will be invoked, and in there, our custom function execution here will then be executed.

That's how this works.

That's what you also already saw multiple times throughout this course, but it is, of course, important to be fully aware of this pattern and to understand this pattern.

So therefore, that will give us this selected answer, and now we can update our state based on that answer.

Now, of course, this state will be an array, and we definitely don't wanna lose the old answers, so the answers that have previously been selected for other questions.

And therefore, we wanna update this state with this function form, where we pass a function to the state updating function because we wanna update this state based on the previous version of this state.

And whenever you do that, you learned in this course that you should use this function form here.

And here we get our previous userAnswers, so the old version of that state, the guaranteed latest version of this state, to be precise.

And we then wanna return our updated state, which should be a new array where we spread in all those existing userAnswers, but where we then at the end append the selected answer as a new element.

That's how this state here should be updated to make sure that we don't lose any old state and that we got the guaranteed latest state.

**Quiz.jsx** component file become :

```javascript
import { useState } from 'react';

import QUESTIONS from '../questions.js';

export default function Quiz() {
    const [userAnswers, setUserAnswers] = useState([]);

    const activeQuestionIndex = userAnswers.length;

    function handleSelectAnswer(selectedAnswer) {
        setUserAnswers((prevUserAnswers) => {
            return [...prevUserAnswers, selectedAnswer];
        });
    }

    return (
        <div id='question'>
            <h2>{QUESTIONS[activeQuestionIndex].text}</h2>
            <ul id='answers'>
                {QUESTIONS[activeQuestionIndex].answers.map((answer) => (
                    <li key={answer} className='answer'>
                        <button onClick={() => handleSelectAnswer(answer)}>{answer}</button>
                    </li>
                ))}
            </ul>
        </div>
    )
}
```

And with all that out of the way, we can go to the App component now, and finally now import the Quiz component from ./components/Quiz.jsx.

**App.jsx** file :

```javascript
import Header from "./components/Header.jsx";
import Quiz from "./components/Quiz.jsx";

function App() {
    return (
        <>
            <Header />
            <main>
                <Quiz />
            </main>
        </>
    )
}

export default App;
```

And then here, besides outputting the Header, we also wanna output the Quiz, and therefore we'll need this special Fragment component that's built into React so that we can have the Header as one element and the Quiz as another element here so that we output them side by side.

And I'll actually also wrap my Quiz into the built-in main element like this just to separate them and for styling purposes.

And therefore now with all that added, if you save everything, you should see something like this on the screen.

![alt text](image-1.png)

You see the answers and you see the questionnaire.

Now the styling is actually a bit off, and to fix this, we can go to the Quiz.jsx file.

And there I actually wanna add another div around my question here, so move this question div into this div, and give this div an ID of quiz.

And the codes of **Quiz.jsx** become like hits after wrapped or adding div and the id='quiz' :

```javascript
import { useState } from 'react';

import QUESTIONS from '../questions.js';

export default function Quiz() {
    const [userAnswers, setUserAnswers] = useState([]);

    const activeQuestionIndex = userAnswers.length;

    function handleSelectAnswer(selectedAnswer) {
        setUserAnswers((prevUserAnswers) => {
            return [...prevUserAnswers, selectedAnswer];
        });
    }

    return (
        <div id='quiz'>
            <div id='question'>
            <h2>{QUESTIONS[activeQuestionIndex].text}</h2>
            <ul id='answers'>
                {QUESTIONS[activeQuestionIndex].answers.map((answer) => (
                    <li key={answer} className='answer'>
                        <button onClick={() => handleSelectAnswer(answer)}>{answer}</button>
                    </li>
                ))}
            </ul>
        </div>
        </div>
    )
}
```

We'll need that because later I'll add more elements to the quiz besides this question.

But with this extra div wrapper here, you see that now this is all nicely centered.

We got this nice box here.

We can select those answers, and we progress through those different questions as we pick answers.

Now of course at the moment, at some point of time, we'll simply exhaust this array of questions, and therefore the app will crash with an error.

![alt text](image-2.png)

But we'll fix that soon because of course we got a lot of logic to add to this project.

But showing those questions and selecting those answers already works.
</details>