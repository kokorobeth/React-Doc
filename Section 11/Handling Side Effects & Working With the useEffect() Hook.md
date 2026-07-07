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

<details>
<summary>Not All Side Effects Need useEffect</summary>

Now before we dive deeper into useEffect and see more examples for useEffect and take a look at the dependencies array again, I wanna make it very clear that, not all side effects require the usage of useEffect because overusing useEffect and using it unnecessarily is considered a bad practice because you must not forget that this is an extra execution cycle that's triggered after the App component or whichever component you're working in execution cycle. So you wanna avoid using useEffect if you don't need it.

And here's an example where we don't need it. Let's say here in handleSelectPlace, we don't just wanna update the state to add a place to our list of places here when we click on it but we also wanna store that selected place and the entire list of selected places in our browsers storage. So that when we reload the app, we don't lose these places, but they're instead still there. That's something we might want to do.

And to do that we can use another function that's built into the browser. We can use the localStorage object which just like navigator is provided by the browser. So localStorage is not coming from React, not built by me, is coming from the browser.

And localStorage allows us to use the setItem method to store some data in the browser's storage and that data will also be available if we leave the website and come back to it later, or if we reload the website.

Now, localStorage is relatively easy to use. You just pass an identifier to setItem, for example, selectedPlaces, and then as a second argument, you pass the value that should be stored. Though it's important to mention that, this data must be in string format. So you can't store an array or object, instead, that data must be converted to a string first which you, for example, can do with the built in JSON.stringify method.

This also is a method and an object that is provided by the browser. JSON.stringify for example, takes an array and will convert that to a string so that it can be stored.

And the array I wanna pass to JSON.stringify here, should be an array of place IDs I selected, let's say. So this id which we're getting here and all the previously storedIds. Therefore, I also need to get all those previously storedIds. And we can do that with a localStorage.getItem. And then of course we have to use the same key as we use for storing, that will then extract the data from localStorage and it will extract it in string format of course, because that's how the data is stored.

So to convert it back to an array, for example we again have to use the JSON object but now the parse method which is basically the opposite of the Stringify method.

Now of course, we might not have any stored places yet and therefore, I'll add some fallback code here which produces an empty array if this here should yield undefined. And this then gives us our storedIds and we can then use these storedIds here to spread them into this array, which we wanna store now and add the new Id of the place that was just selected in front of the storedIds.

So besides updating that data in my state in the currently running application, which I do in order to update the UI, I am also storing this list of IDs here in this case in my localStorage.

I also wanna make sure that I don't store an already existing id again in this list here. And therefore, we can add a if check and check if storedIds already contains this ID here. So this ID I'm getting as an argument we can do that with indexOf. And if that yields minus one, it means this ID is not part of storedIds yet and therefore in that case, I want to update the stored data. Otherwise I don't wanna do anything.

Now all this code here in the end, is just another example for a side effect because just as fetching the user's location, 

**App.jsx** component file on function handleSelectPlace :

```javascript
function handleSelectPlace(id) {
    setPickedPlaces((prevPickedPlaces) => {
      if (prevPickedPlaces.some((place) => place.id === id)) {
        return prevPickedPlaces;
      }
      const place = AVAILABLE_PLACES.find((place) => place.id === id);
      return [place, ...prevPickedPlaces];
    });

    const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || []; // codes adding until below
    if(storedIds.indexOf(id) === -1) { 
      localStorage.setItem(
        'selectedPlaces', 
        JSON.stringify([id, ...storedIds])
      );
    }
  }
```

this code down here where we store data in the browser's storage is not directly related to rendering this JSX code. Updating this state here is, because those state updates, directly lead to a new JSX snapshot in the end. But this storage here is totally unrelated. Still it is of course code that's needed in this application to add this feature where I wanna persist this list of places that's created by the user. So having this code here is not bad. That's again, really important to understand but it is a side effect.

Now, unlike with the navigator code here we don't need to wrap this code down here with useEffect though. And indeed we can't use useEffect here because we're inside of a function. And this usage here would violate the rules of hooks because you're not allowed to use React hooks in nested functions, if statements or anything like that. They must be used directly in the root level of your component function, like we're using it here.

But we also don't need useEffect down here because there's nothing wrong with executing this code here because this code gets executed when this function here the handleSelectPlace function is executed which in the end happens when the user clicks on one of these items. And then this code does not enter an infinite loop because we're not updating any state here.

And even if we were updating any state in relation to that localStorage data storage. Even if we would do that, we would not create an infinite loop because again, this code in this handleSelectPlace function only executes when a user clicks on one of these items not when the App component function is re-executed.

So unlike this navigator code, which had to run when that component function code executed, this localStorage data storage code, does only run upon user interaction and therefore, doesn't create an infinite loop. Even if we would be updating some state here.

And that's really important to understand. Not every side effect needs useEffect. You basically only need the useEffect hook to prevent infinite loops or if you have code that can only run after the component function executed at least once. And I'll show you an example for this a little bit later. But here, this localStorage code here is totally fine.

full codes of **App.jsx** component file :

```javascript
import { useRef, useState, useEffect } from 'react';

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

    const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || [];
    if(storedIds.indexOf(id) === -1) {
      localStorage.setItem(
        'selectedPlaces', 
        JSON.stringify([id, ...storedIds])
      );
    }
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
          fallbackText={"Sorting places by distance..."}
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
<summary>useEffect Not Needed: Another Example</summary>

Now before we'll take another look at useEffect, let's stick at this local storage example here, because of course just storing items when we add them is not enough. The local storage should also be updated when we remove a place, by clicking on it here and confirming this. And of course, I also wanna load my data from local storage when the app starts, so that when that happens I pre-populate this box up here with my stored items.

Now let's start with the code for deleting items from local storage. To do that, we again first need to fetch our stored IDs, so that we can then update them. And then we again need to update the stored items with a local storage setItem and update them with help of this key.

And now the updated array in the end is based on the fetched existing array of data. And here we again need to create a stringified array and I'll create that array that should now be stored based on that stored IDs array with help of the filter method, which is built into the browser, basically, and which allows us to produce a new array, based on this array, and some filtering condition.

For that filter takes a function that will be executed on every item in this array, and will get every item as an input to this function here. And then we have to return true, if we want to keep that item, and false if we want drop it.

So therefore here, I'll simply check if the ID I am looking at here is not equal to selectedPlace.current, which is simply the ID of the place on which I clicked here, when I'm clicking on it in my first box. So if these two IDs do not match, I know that this is not the item I wanna delete, therefore I'm returning true and I keep the item. But if these IDs do match, this condition here will yield false and this ID will be removed from this array. And that's how we can store an updated array that does no longer contain this ID.

**App.jsx** component file 
```javascript
function handleRemovePlace() {
    setPickedPlaces((prevPickedPlaces) =>
      prevPickedPlaces.filter((place) => place.id !== selectedPlace.current)
    );
    modal.current.close();

    const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || []; // codes to bottom added
    localStorage.setItem('selectedPlaces', JSON.stringify(storedIds.filter((id) => id !== selectedPlace.current)))
  }
```

Now last but not least, we of course also need to fetch these items when the app starts. 
And here you might again think that you probably need useEffect, because of course we could now use useEffect, just as we used it here with navigator geolocation. And we could merge our code into this existing useEffect usage, or use it again, like all React hooks, you can use useEffect as often as you want and need to.

And you could therefore think that the code for retrieving our places should go into useEffect here. So we can get our loaded places just as we're doing it down here, with help of local storage getItem, like this.

And since these are only the IDs, but I want to get places with all the place related data, like the title and the image, we then need to map these IDs to actual place objects. By using the map method, for example, to convert every ID to a complete place object.

And that can be done by taking this available places array, which is coming from the data JS file, which contains these place objects. And it's these objects to which I wanna map my IDs, and we can perform that mapping by using available places here, and by then finding a place for the ID we're having here.

So find then also takes another function. And here we get every place from AVAILABLE_PLACES passed in automatically. And here I'm looking for the place where the ID is equal to this ID. And this code here will then simply give us an array of place objects based on this array of IDs, which we retrieve from local storage.

And of course now we could call setPickedPlaces here and set this equal to storedPlaces. Now when we add an empty dependencies array, just as we did it down here, this effect function here will only run once after the app component function ran. And therefore will not enter an infinite loop, will fetch our data and populate our box with that fetched data.

```javascript
function App() {
  const modal = useRef();
  const selectedPlace = useRef();
  const [availablePlaces, setAvailablePlaces] = useState([]);
  const [pickedPlaces, setPickedPlaces] = useState([]);

  useEffect(() => {
    const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || [];
    const storedPlaces = storedIds.map(id => 
      AVAILABLE_PLACES.find((place) => place.id === id)
    );

    setPickedPlaces(storedPlaces);
  }, []);
```

We could do it like that. And if I save that and I reload, you see indeed, I'm starting with the places I previously added here. And if I delete a place and I reload, that place is gone but the other places are still fetched. So this clearly works.

But this here is now an example for a redundant usage of useEffect. Now, why is using useEffect like this redundant and actually not recommended?

Because this code here, where we use local storage, unlike this code here where we gut the user's location, runs synchronously. Which means it basically finishes instantly. It's executed line by line and once a line finished execution, it's done. We have the final result.

And this was not the case here for getCurrentPosition, when this line executed here it was not done yet. Instead it was only done once this callback function here was executed by the browser and that happened at some point in the future. We can even see that it takes some time if we reload because these places down here are not there instantly.

But for local storage, that's not the case. We got no callback function or promise or anything like that here. Instead retrieving the data like this is instant. And therefore this app component function does not finish its execution cycle before fetching that data is done.

We can therefore simply get rid of useEffect and get rid of that state updating function here, which would be a problem, because it would lead to an infinite loop. And we can simply move that code in front of the state initialization code and use the stored places, which again are available instantly here, to initialize our picked places state like this. So to use the stored places as an initial state value.

**App.jsx** file :
```javascript
function App() {

  const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || [];
  const storedPlaces = storedIds.map(id =>  // this line until ; is moved from useEffect before.
    AVAILABLE_PLACES.find((place) => place.id === id)
  );

  const modal = useRef();
  const selectedPlace = useRef();
  const [availablePlaces, setAvailablePlaces] = useState([]);
  const [pickedPlaces, setPickedPlaces] = useState(storedPlaces); // updated the parameter
```

This works because this code runs synchronously and does not take some time to finish, during which the app component function execution would finish. That's not the case here.

And we can actually even move that code out of the app component function, so that it only runs once in the entire application lifecycle, when this code file is parsed and executed for the first time.

```javascript
const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || [];
const storedPlaces = storedIds.map(id => 
  AVAILABLE_PLACES.find((place) => place.id === id)
);

function App() {

  const modal = useRef();
  const selectedPlace = useRef();
  const [availablePlaces, setAvailablePlaces] = useState([]);
  const [pickedPlaces, setPickedPlaces] = useState(storedPlaces);
```

Because there's no reason to put this into the app component, which would only mean that it runs again and again every time the app component function is executed, which in the end means that we're wasting some performance.

Instead, it's enough to run this once when the overall app starts and then we can still use stored places in the component function, because this component function execution will run after this code in front of it.

And therefore, if we change the code like this and we save this and reload, we're still fetching our places here. So this is still working and we can still manipulate them and of course also delete places, that all works.

But now with side effects that don't need useEffect.

The full code of **App.jsx** become :

```javascript
import { useRef, useState, useEffect } from 'react';

import Places from './components/Places.jsx';
import { AVAILABLE_PLACES } from './data.js';
import Modal from './components/Modal.jsx';
import DeleteConfirmation from './components/DeleteConfirmation.jsx';
import logoImg from './assets/logo.png';
import { sortPlacesByDistance } from './loc';

const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || [];
const storedPlaces = storedIds.map(id => 
  AVAILABLE_PLACES.find((place) => place.id === id)
);

function App() {

  const modal = useRef();
  const selectedPlace = useRef();
  const [availablePlaces, setAvailablePlaces] = useState([]);
  const [pickedPlaces, setPickedPlaces] = useState(storedPlaces);

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

    const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || [];
    if(storedIds.indexOf(id) === -1) {
      localStorage.setItem(
        'selectedPlaces', 
        JSON.stringify([id, ...storedIds])
      );
    }
  }

  function handleRemovePlace() {
    setPickedPlaces((prevPickedPlaces) =>
      prevPickedPlaces.filter((place) => place.id !== selectedPlace.current)
    );
    modal.current.close();

    const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || [];
    localStorage.setItem('selectedPlaces', JSON.stringify(storedIds.filter((id) => id !== selectedPlace.current)))
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
          fallbackText={"Sorting places by distance..."}
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
<summary>Preparing Another Use-Case For useEffect</summary>

So now that we got started with side effects that need and that don't need useEffect, let's take a closer look at useEffect and especially at this dependencies array.

And for that, let's switch to this modal component. In there I got some code using the useImperativeHandle hook that ensures that we expose two methods, two functions, to the outside world here, a open and a closed function. And these functions will then internally, in this modal component, show or close the dialog element, which is also controlled with help of our ref here.

So these exposed functions, these methods here, are used in the app component. There I have code where I call open and I have code where I call close. And my goal now is to actually handle this with help of an effect, with help of a side effect. So with help of the useEffect hook, because as you'll see, that's all the possible in situations like this.

The full code of **Modal.jsx** file before updated :

```javascript
import { forwardRef, useImperativeHandle, useRef } from 'react';
import { createPortal } from 'react-dom';

const Modal = forwardRef(function Modal({ children }, ref) {
  const dialog = useRef();

  useImperativeHandle(ref, () => {
    return {
      open: () => {
        dialog.current.showModal();
      },
      close: () => {
        dialog.current.close();
      },
    };
  });

  return createPortal(
    <dialog className="modal" ref={dialog}>
      {children}
    </dialog>,
    document.getElementById('modal')
  );
});

export default Modal;

```

And therefore here I'll get rid of this useImperativeHandle code, I'll delete it. And also delete this import. And also get rid of this ref prop because I don't need it anymore.

And what we could now do as an alternative to the old approach is that this modal component accepts a prop, let's say a prop named open, though the name, of course, is totally up to you.

Now as it turns out, the dialog element also has a open prop built into this element which we could then set to our open prop assuming that open is true or false, because that is what the open prop of the dialog element wants.


**Modal.jsx** file component

```javascript
import { useRef } from 'react';
import { createPortal } from 'react-dom';

const Modal = forwardRef(function Modal({ open, children }) {
  const dialog = useRef();

  return createPortal(
    <dialog className="modal" ref={dialog} open={open}>
      {children}
    </dialog>,
    document.getElementById('modal')
  );
});

export default Modal;

```

And with that change, we could go back to the app component. And now instead of opening and closing that modal with help of the modal ref, we could delete this ref 

```javascript
function App() {
  // const modal = useRef(); // deteled
  const [modalIsOpen, setModalIsOpen] = useState(false);
  const selectedPlace = useRef();
  const [availablePlaces, setAvailablePlaces] = useState([]);
  const [pickedPlaces, setPickedPlaces] = useState(storedPlaces);
```
and instead manage some extra state here which controls whether the modal should be open or not.

```javascript
function App() {
  const [modalIsOpen, setModalIsOpen] = useState(false);
  const selectedPlace = useRef();
  const [availablePlaces, setAvailablePlaces] = useState([]);
  const [pickedPlaces, setPickedPlaces] = useState(storedPlaces);
```

Initially it should be false so that the modal is not open. And here we could say IsOpen and set IsOpen. And maybe name it ModalIsOpen to be clear what exactly is open or not.

And now in all the places where I called open, we should now call setModalIsOpen and set it to true. And in all the places where we called close, we should now call setModalIsOpen and set it to false. Of course, also down here.

**App.jsx** file component

*From*

```javascript
function handleStartRemovePlace(id) {
    modal.current.open();
    selectedPlace.current = id;
  }

  function handleStopRemovePlace() {
    modal.current.close();
  }
```

also in funcion below :

```javascript
function handleRemovePlace() {
    setPickedPlaces((prevPickedPlaces) =>
      prevPickedPlaces.filter((place) => place.id !== selectedPlace.current)
    );
    modal.current.close();
```

And changed into :

```javascript
function handleRemovePlace() {
    setPickedPlaces((prevPickedPlaces) =>
      prevPickedPlaces.filter((place) => place.id !== selectedPlace.current)
    );
    modal.current.close();
```
**Into :**

```javascript
function handleStartRemovePlace(id) {
    setModalIsOpen(true); // changed
    selectedPlace.current = id;
  }

  function handleStopRemovePlace() {
    setModalIsOpen(false); // changed
  }
```

aslo this function :

```javascript
function handleRemovePlace() {
    setPickedPlaces((prevPickedPlaces) =>
      prevPickedPlaces.filter((place) => place.id !== selectedPlace.current)
    );
    setModalIsOpen(false); // changed
```

Now we can use the modalIsOpen state and pass it as a value to this open prop. modalIsOpen. And we should remove this ref here because we don't have this modal ref anymore.

**App.jsx** file :

*From :*
```javascript
return (
    <>
      <Modal ref={modal}>
        <DeleteConfirmation
          onCancel={handleStopRemovePlace}
          onConfirm={handleRemovePlace}
        />
      </Modal>
```

*Into :*
```javascript
  return (
    <>
      <Modal open={modalIsOpen}>
        <DeleteConfirmation
          onCancel={handleStopRemovePlace}
          onConfirm={handleRemovePlace}
        />
      </Modal>
```


If we save that, you'll see that if I now click on an item, the modal does indeed open, but the backdrop is actually missing. This area behind the modal that grays out the page and makes sure that we can't interact with the rest of the page.

This backdrop is missing. And it's missing because this backdrop is only added by the dialog element if we open it by calling the dialog's showModal method. Only when we call this method will this backdrop be added.

the code of **Modal.jsx** changed into below 
Here the full codes of *Modal.jsx*

```javascript
import { useRef } from 'react';
import { createPortal } from 'react-dom';

function Modal({ open, children }) {
  const dialog = useRef();

  dialog.current.showModal();

  return createPortal(
    <dialog className="modal" ref={dialog}>
      {children}
    </dialog>,
    document.getElementById('modal')
  );
};

export default Modal;


```

So therefore forwarding this open prop to the dialog as we're currently doing it does not really work. But we can still stick to this prop focused solution by again using useEffect.

full codes of **App.jsx** component file :

```javascript
import { useRef, useState, useEffect } from 'react';

import Places from './components/Places.jsx';
import { AVAILABLE_PLACES } from './data.js';
import Modal from './components/Modal.jsx';
import DeleteConfirmation from './components/DeleteConfirmation.jsx';
import logoImg from './assets/logo.png';
import { sortPlacesByDistance } from './loc';

const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || [];
const storedPlaces = storedIds.map(id => 
  AVAILABLE_PLACES.find((place) => place.id === id)
);

function App() {
  const [modalIsOpen, setModalIsOpen] = useState(false);
  const selectedPlace = useRef();
  const [availablePlaces, setAvailablePlaces] = useState([]);
  const [pickedPlaces, setPickedPlaces] = useState(storedPlaces);

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

  function handleStartRemovePlace(id) {
    setModalIsOpen(true);
    selectedPlace.current = id;
  }

  function handleStopRemovePlace() {
    setModalIsOpen(false);
  }

  function handleSelectPlace(id) {
    setPickedPlaces((prevPickedPlaces) => {
      if (prevPickedPlaces.some((place) => place.id === id)) {
        return prevPickedPlaces;
      }
      const place = AVAILABLE_PLACES.find((place) => place.id === id);
      return [place, ...prevPickedPlaces];
    });

    const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || [];
    if(storedIds.indexOf(id) === -1) {
      localStorage.setItem(
        'selectedPlaces', 
        JSON.stringify([id, ...storedIds])
      );
    }
  }

  function handleRemovePlace() {
    setPickedPlaces((prevPickedPlaces) =>
      prevPickedPlaces.filter((place) => place.id !== selectedPlace.current)
    );
    setModalIsOpen(false);

    const storedIds = JSON.parse(localStorage.getItem('selectedPlaces')) || [];
    localStorage.setItem('selectedPlaces', JSON.stringify(storedIds.filter((id) => id !== selectedPlace.current)))
  }

  return (
    <>
      <Modal open={modalIsOpen}>
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
          fallbackText={"Sorting places by distance..."}
          onSelectPlace={handleSelectPlace}
        />
      </main>
    </>
  );
}

export default App;
```
</details>