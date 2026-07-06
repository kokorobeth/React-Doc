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