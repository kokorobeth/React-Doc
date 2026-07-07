<details>
<summary>Module Introduction & Starting Project</summary>

In this course section, we'll work on this Placepicker application here,which allows us to pick places we eventually might wanna visit. And it also allows us to get rid of places if we decide we don't want to go there. And whilst working on this application, and whilst enhancing this application throughout this section, we are going to dive into a super important React concept.

Because in this section, you will learn how to deal with side effects in React apps,and you'll learn what exactly side effects are and how you can manage them.

And for that you will learn how to tackle side effects and why in certain situations React's useEffect hook might be a good choice. You will of course learn how to use that hook, how to manage its dependencies, and what exactly that is. And you will also learn when not to use useEffect. But of course at this point, this all probably sounds rather confusing and abstract. And therefore let's dive right in. Let me show you a side effect and why in certain use cases you need that useEffect hook. And of course also how you use it. Now for this section, I prepared this application here for you, and this starting project actually already works quite well. You can view places, you can select places, and you can delete places. Nonetheless, we're going to enhance this application throughout this section and also add more features to it.

And therefore, as always basically, attached you'll find this starting project, both a local and a code sandbox version. For the local version, as always, you should run npm install and then npm run dev. For the code sandbox version, this is not required.

Now if you take a look at this project code, you'll notice that it has a couple of components which are relatively straightforward. They use features you already learned about like state and refs, and the modal component uses useImperativeHandle here to expose some functions through a ref. And that ref here is received and extracted as a prop. Alternatively, this component could also be set up with help of forwardRef, but since this project uses a React version high enough to not need that, this component indeed is created without forwardRef.

So these therefore, in the end, of course, are all features you already learned about earlier in the course. And overall, this application code should be relatively straightforward and nothing new. In the end, it's just about managing this array of picked places here by adding or removing places depending on where the user clicked.

But you'll also notice that this starting project also comes with a data.js file, which includes a bunch of dummy data responsible for outputting these place cards here in the end. And a loc.js file, which contains some location calculation logic, which we'll need throughout this section. And it's indeed this file, or specifically this function, which we'll need in the next lecture where we will also meet our first side effect.

**Summary**

**Dealing with Side Effects**
*Keeping the UI Synchronized*

- Understanding side effects & useEffect()
- Effects & Dependencies
- When NOT to use useEffect()

</details>

<details>
<summary>What's a "Side Effect"? A Thorough Example</summary>

So what exactly are side effects?

Well, in the end, side effects are tasks you could say that need to be executed in your app in order for the app to work correctly but tasks that don't directly impact the current component render cycle. That's what a side effect is in the end in the context of a React app. So whenever you have a task that must be performed but that does not directly and instantly impact the current component render cycle. And that's, of course still pretty vague.

So let me give you an example. And let's say for example in this demo app, we actually wanna sort these available places down there by distance to the user of the website. So if you are living near the Sahara Desert, this card should come first and the other cards should be sorted by distance to your location. That's my idea here.

Now, that's why I'm providing this loc.js file because in there I already prepare a function that allows us to calculate the distance between two points on the earth where every point is described through a latitude and longitude coordinate. And I'm exporting a sort places by distance utility function here which takes an array of places as input, so places as they are defined in the data.js file and which then in the end, gives me that same list just sorted by distance to the user's location.

But that of course implies one important thing. We need to get the location of the user of this website. And thankfully, that's at least in theory, not too difficult in the browser. Because there's a built-in browser method you can call to get that location.

Now, for that, we could go into the app component because, of course I want to get this location as early as possible when this app starts up essentially. Then I want to get the user's location. And as you know, this app component is the root component in most React apps, and this React app is no exception. So therefore this app component functions sounds like a great place to get the user's location.

So we could go there and then maybe here, we could add that code to get the user's location, which in the browser, involves the usage of the navigator object, an object exposed by the browser to our JavaScript code that runs in the browser. So navigator is not defined by me, it's not built into React, it's provided by the browser instead.

**App.jsx** file component

```javascript
  navigator.geolocation.getCurrentPosition((position) => {
    const sortedPlaces = sortPlacesByDistance(
      AVAILABLE_PLACES,
      position.coords.latitude,
      position.coords.longitude
    );
  });
```

Now, this globally available navigator object then has a geolocation object which then has a get current position method which we can call to get the current position of the user of the website. Now, when we call this method, the user will be asked for permission to get their location and then once that permission is granted, this will go ahead and fetch this location.

Now of course, fetching that location can take some time though, and therefore, get current position takes a so-called callback function. It takes a function as an input. For example, an anonymous arrow function as I'm defining it here, which will be executed by the browser once the location has been fetched, which can be the case after a couple of milliseconds or maybe even a couple of seconds if it's slow.

So the code that depends on this location should be executed inside of this function because it's dysfunction that will be called by the browser once the location has been determined. So it's in here where I want to call sortPlacesByDistance. So this function I'm exporting in loc.js and therefore, of course we should import it here. We should import sortPlacesByDistance from loc.js so that we can call it here.

And then to this function, we must pass our available places, which is this array imported from the data.js file. So this array of dummy places. And then we also must provide the latitude and longitude coordinates of the user. Now that's what we get from get current position and the browser exposes the fetched position to us through a position object, which it automatically passes to this function.

Keep in mind that this function will be called by the browser and it's then the browser that also gives us this object which includes this user's position. So we can use this position object to then access the coords nested object and then there the latitude. And as a third argument to sort places by distance, we pass position coords longitude. So that we're passing the user's latitude and longitude coordinates to this sort places by distance function.

Now this will then return these sorted places array, which we can now use in this application. And that's now where things get tricky. Because this here, this entire code is actually a side effect. It's a side effect because this code is, of course needed by this application, we need the user's location after all but it's not directly related to the task, to the main goal of this component function.

Because the main goal of every component function is to return renderable JSX code. Now this code here is a side effect because it's not directly related with that task. All the other code in this component is related because we're setting up click listeners, which we need in our JSX code, we're setting up the state which impacts what we see on the screen. But this code where we fetch a user's location is not directly related.

Especially also because this code here does not finish instantly. Instead, this callback function will be called at some point in the future where this app component function most likely finished its execution already. And that's why this here is a side effect.

*Full Codes* of **App.jsx** component file :

```javascript
import { useRef, useState } from 'react';

import Places from './components/Places.jsx';
import { AVAILABLE_PLACES } from './data.js';
import Modal from './components/Modal.jsx';
import DeleteConfirmation from './components/DeleteConfirmation.jsx';
import logoImg from './assets/logo.png';
import { sortPlacesByDistance } from './loc';

function App() {
  const modal = useRef();
  const selectedPlace = useRef();
  const [pickedPlaces, setPickedPlaces] = useState([]);

  navigator.geolocation.getCurrentPosition((position) => {
    const sortedPlaces = sortPlacesByDistance(
      AVAILABLE_PLACES,
      position.coords.latitude,
      position.coords.longitude
    );
  });

  function handleStartRemovePlace(id) {
    modal.current.open();
    selectedPlace.current = id;
  }

  function handleStopRemovePlace() {
    modal.current.close();
  }

  function handleSelectPlace(id) {
    setPickedPlaces((prevPickedPlaces) => {
      if (prevPickedPlaces.some((place) => place.id === id)) {
        return prevPickedPlaces;
      }
      const place = AVAILABLE_PLACES.find((place) => place.id === id);
      return [place, ...prevPickedPlaces];
    });
  }

  function handleRemovePlace() {
    setPickedPlaces((prevPickedPlaces) =>
      prevPickedPlaces.filter((place) => place.id !== selectedPlace.current)
    );
    modal.current.close();
  }

  return (
    <>
      <Modal ref={modal}>
        <DeleteConfirmation
          onCancel={handleStopRemovePlace}
          onConfirm={handleRemovePlace}
        />
      </Modal>

      <header>
        <img src={logoImg} alt="Stylized globe" />
        <h1>PlacePicker</h1>
        <p>
          Create your personal collection of places you would like to visit or
          you have visited.
        </p>
      </header>
      <main>
        <Places
          title="I'd like to visit ..."
          fallbackText={'Select the places you would like to visit below.'}
          places={pickedPlaces}
          onSelectPlace={handleStartRemovePlace}
        />
        <Places
          title="Available Places"
          places={AVAILABLE_PLACES}
          onSelectPlace={handleSelectPlace}
        />
      </main>
    </>
  );
}

export default App;
```
</details>

<details>
<summary>A Potential Problem with Side Effects: An Infinite Loop</summary>

Now, it's not necessarily a problem to have a side effect and to have code like this in your component function, but it will get a problem here and I'll show you why.

Because, of course, now that we got the sortedPlaces, we wanna use these sortedPlaces to show them on the screen. Specifically, it's this usage of the places component where instead of these dummy available places, I now wanna pass my sorted available places as input.

And, of course, those sorted places, as I just explained, are not available right at the start because this operation of getting the user's location will take some time. So the first app component render cycle will be finished at the point of time where we have this location.

Therefore, we need state here. We need a state that in the end manages the available places, so the availablePlaces and a setAvailablePlaces updating function. So that we start with an empty array and we set this state to these sorted places once we have them.

**App.jsx** component file :

```javascript
function App() {
  const modal = useRef();
  const selectedPlace = useRef();
  const [availablePlaces, setAvailablePlaces] = useState([]); // adding useState codes
  const [pickedPlaces, setPickedPlaces] = useState([]);

  navigator.geolocation.getCurrentPosition((position) => {
    const sortedPlaces = sortPlacesByDistance(
      AVAILABLE_PLACES,
      position.coords.latitude,
      position.coords.longitude
    );

    setAvailablePlaces(sortedPlaces); // also adding here
  });
```

 So once this operation of fetching the user's location finished and since this then triggers a new render cycle, the state will be updated with those sorted places and we can pass the available places to this second places component here instead of the raw dummy data.

 **App.jsx** compoent file :

 ```javascript
      <main>
        <Places
          title="I'd like to visit ..."
          fallbackText={'Select the places you would like to visit below.'}
          places={pickedPlaces}
          onSelectPlace={handleStartRemovePlace}
        />
        <Places
          title="Available Places" 
          places={availablePlaces} // this changed from AVAILABLE_PLACES
          onSelectPlace={handleSelectPlace}
        />
      </main>
 ```

That looks like a good solution, but this solution actually has a flaw because it would cause an infinite loop. And why is that?

Well, because we're updating the state here, and as you learned, calling such a state updating function tells React to re-execute the component function to which the state belongs, so this app component in this case.

Now, what happens if this component function executes again? Well, we fetch the user's location again and then we set the state and we execute the component function again and we fetch the location again and we set the state and you see where that is going. That will be an infinite loop and that would crash our application.

And that's therefore an example for a side effect which when used like this causes a problem. And that's where the useEffect hook comes into play because that hook allows us to solve that problem.

Full codes of **App.jsx** component file 

```javascript
import { useRef, useState } from 'react';

import Places from './components/Places.jsx';
import { AVAILABLE_PLACES } from './data.js';
import Modal from './components/Modal.jsx';
import DeleteConfirmation from './components/DeleteConfirmation.jsx';
import logoImg from './assets/logo.png';
import { sortPlacesByDistance } from './loc';

function App() {
  const modal = useRef();
  const selectedPlace = useRef();
  const [availablePlaces, setAvailablePlaces] = useState([]);
  const [pickedPlaces, setPickedPlaces] = useState([]);

  navigator.geolocation.getCurrentPosition((position) => {
    const sortedPlaces = sortPlacesByDistance(
      AVAILABLE_PLACES,
      position.coords.latitude,
      position.coords.longitude
    );

    setAvailablePlaces(sortedPlaces);
  });

  function handleStartRemovePlace(id) {
    modal.current.open();
    selectedPlace.current = id;
  }

  function handleStopRemovePlace() {
    modal.current.close();
  }

  function handleSelectPlace(id) {
    setPickedPlaces((prevPickedPlaces) => {
      if (prevPickedPlaces.some((place) => place.id === id)) {
        return prevPickedPlaces;
      }
      const place = AVAILABLE_PLACES.find((place) => place.id === id);
      return [place, ...prevPickedPlaces];
    });
  }

  function handleRemovePlace() {
    setPickedPlaces((prevPickedPlaces) =>
      prevPickedPlaces.filter((place) => place.id !== selectedPlace.current)
    );
    modal.current.close();
  }

  return (
    <>
      <Modal ref={modal}>
        <DeleteConfirmation
          onCancel={handleStopRemovePlace}
          onConfirm={handleRemovePlace}
        />
      </Modal>

      <header>
        <img src={logoImg} alt="Stylized globe" />
        <h1>PlacePicker</h1>
        <p>
          Create your personal collection of places you would like to visit or
          you have visited.
        </p>
      </header>
      <main>
        <Places
          title="I'd like to visit ..."
          fallbackText={'Select the places you would like to visit below.'}
          places={pickedPlaces}
          onSelectPlace={handleStartRemovePlace}
        />
        <Places
          title="Available Places"
          places={availablePlaces}
          onSelectPlace={handleSelectPlace}
        />
      </main>
    </>
  );
}

export default App;
```
</details>

<details>
<summary>Using useEffect for Handling (Some) Side Effects</summary>

So, how can we use "React useEffect Hook" to get rid of this problem? So, to handle this side effect in a better way.

Well, first of all, we have to import it. useEffect from React.

```javascript
import { useRef, useState, useEffect } from 'react'; // --> import useEffect

import Places from './components/Places.jsx';
import { AVAILABLE_PLACES } from './data.js';
import Modal from './components/Modal.jsx';
import DeleteConfirmation from './components/DeleteConfirmation.jsx';
import logoImg from './assets/logo.png';
import { sortPlacesByDistance } from './loc';

function App() {
```

And with it imported like all hooks, this hook must be executed in the component function, in the app component function.

Now, useEffect, unlike useState or useRef does not return a value, though. Instead, useEffect needs two arguments. And the first argument is a function that should wrap your side effect code. So, in this case here, I'm creating an anonymous function and I move my location fetching state updating code into this anonymous function. That's the first step, but that's not all we have to do.

Instead, you should also pass second argument to useEffect. So, after this anonymous function, and that second argument is an array of dependencies of that effect function. And I'll get back to these dependencies later. For now, just add an empty array.

```javascript
function App() {
  const modal = useRef();
  const selectedPlace = useRef();
  const [availablePlaces, setAvailablePlaces] = useState([]);
  const [pickedPlaces, setPickedPlaces] = useState([]);

  useEffect(() => {
    navigator.geolocation.getCurrentPosition((position) => {
      const sortedPlaces = sortPlacesByDistance(
        AVAILABLE_PLACES,
        position.coords.latitude,
        position.coords.longitude
      );

    setAvailablePlaces(sortedPlaces);
    });
  }, []);
```

Now, if you do that, if you change the code to look like this, you will not run into this infinite loop problem. And why is that?

Because the idea behind useEffect is that this function which you pass as a first argument to useEffect will be executed by React after very important. After every component execution.

So, if the app starts and the app component function executes, this code here will not be executed right away. Instead, it's only after the app component function execution finished. So, after this JSX code here has been returned, that this side effect function you passed to useEffect will be executed by React. So, React will execute that after the component function is done executing.

Now, if you then update the state here, the component function executes again as you learned. And in theory this effect function would execute again. But that's where this dependencies array comes into play.

If you define this dependencies array. So, if you do not omit it, but you define it. Then, React will actually take a look at the dependencies specified there. And it will only execute this effect function again. If the dependency values changed.

Now, this might sound a bit abstract but I'll show you a use case. Where we have a dependency a little bit later. Here, where we have no dependencies. Those dependencies also can't change because we have none. So, they obviously never change.

Therefore, React actually never re-executes this effect function. Instead, it only executes it once after this app component function was executed for the first time. But then this effect function is never executed again.

If you would omit this dependencies array, this effect function would be executed after every app component render cycle. And therefore, we would still have an infinite loop. But with an empty dependencies array, that will not be the case.

And therefore, with this out of the way. We will now set our available places to the sorted available places. Once we have to users' location without creating an infinite loop.

And now, I'll just tweak the application a little bit. And down here on this places component, I'll add the fallback text prop, which is supported by this component and set it to Sorting places by distance. Which is simply some fallback text that will be shown during the time where we don't have any places yet. 

**App.jsx** component file :
```javascript
        <Places
          title="Available Places"
          places={availablePlaces}
          fallbackText={"Sorting places by distance..."} // adding code here
          onSelectPlace={handleSelectPlace}
        />
```

Because we're still looking for the user's location. Because initially of course, we don't have any places here. We start with an empty array.

With all that, If you save that and you reload, you should see a little pop-up here, that asks you for permission to get your location. 

![alt text](image.png)

And if you click block, you'll break the app. So, here, I'll click allow. And with that it'll fetch my location which can take some time as I mentioned. 

![alt text](image-1.png)

But then, it'll present me these places sorted by distance to my location.

Now of course, the order will depend on where you are located. For me, it looks pretty accurate. I'd say, I haven't checked all locations here. And it's just some dummy data anyways, but it looks correct.

There also is no error in the console. And therefore, this code now works. And we're handling this side effect in a way that does not crash our app. Which I guess is always a good thing to have.

</details>