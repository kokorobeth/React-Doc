<details>
<summary>Module Introduction</summary>

**Advanced State Management**
*Beyond Basic App & Lifting Up State*

- The Problem of Shared State : Prop Drilling
- Embracing **Component Composition**
- Sharing State with **Context**
- Managing Complex State with **Reducers**
</details>

<details>
<summary>Understanding Pop Drilling & Project Overview</summary>

Here is the link of the sources we can download for references :

https://github.com/academind/react-complete-guide-course-resources/blob/main/attachments/10%20Advanced%20State%20Management%20with%20Context%20useReducer/01-starting-project.zip

</details>

<details>
<summary>Pop Drilling: Component Composition as a Solution</summary>

do **run npm install** and we'll see the result below :

![alt text](image.png)

Before we run into several components here, these are files to be known :

*App.jsx*

```javascript
import { useState } from 'react';

import Header from './components/Header.jsx';
import Shop from './components/Shop.jsx';
import { DUMMY_PRODUCTS } from './dummy-products.js';

function App() {
  const [shoppingCart, setShoppingCart] = useState({
    items: [],
  });

  function handleAddItemToCart(id) {
    setShoppingCart((prevShoppingCart) => {
      const updatedItems = [...prevShoppingCart.items];

      const existingCartItemIndex = updatedItems.findIndex(
        (cartItem) => cartItem.id === id
      );
      const existingCartItem = updatedItems[existingCartItemIndex];

      if (existingCartItem) {
        const updatedItem = {
          ...existingCartItem,
          quantity: existingCartItem.quantity + 1,
        };
        updatedItems[existingCartItemIndex] = updatedItem;
      } else {
        const product = DUMMY_PRODUCTS.find((product) => product.id === id);
        updatedItems.push({
          id: id,
          name: product.title,
          price: product.price,
          quantity: 1,
        });
      }

      return {
        items: updatedItems,
      };
    });
  }

  function handleUpdateCartItemQuantity(productId, amount) {
    setShoppingCart((prevShoppingCart) => {
      const updatedItems = [...prevShoppingCart.items];
      const updatedItemIndex = updatedItems.findIndex(
        (item) => item.id === productId
      );

      const updatedItem = {
        ...updatedItems[updatedItemIndex],
      };

      updatedItem.quantity += amount;

      if (updatedItem.quantity <= 0) {
        updatedItems.splice(updatedItemIndex, 1);
      } else {
        updatedItems[updatedItemIndex] = updatedItem;
      }

      return {
        items: updatedItems,
      };
    });
  }

  return (
    <>
      <Header
        cart={shoppingCart}
        onUpdateCartItemQuantity={handleUpdateCartItemQuantity}
      />
      <Shop onAddItemToCart={handleAddItemToCart} />
    </>
  );
}

export default App;

```

*Shop.jsx*

```javascript
import { DUMMY_PRODUCTS } from '../dummy-products.js';
import Product from './Product.jsx';

export default function Shop({ onAddItemToCart }) {
  return (
    <section id="shop">
      <h2>Elegant Clothing For Everyone</h2>

      <ul id="products">
        {DUMMY_PRODUCTS.map((product) => (
          <li key={product.id}>
            <Product {...product} onAddToCart={onAddItemToCart} />
          </li>
        ))}
      </ul>
    </section>
  );
}

```

*dummy-proudcts.js*

```javascript
import mochaOvercoat from './assets/mocha-overcoat.jpg';
import dreamGown from './assets/dream-gown.jpg';
import rainJacket from './assets/rain-jacket.jpg';
import merlotSuit from './assets/merlot-suit.jpg';
import moonlightDress from './assets/moonlight-dress.jpg';
import denimPioneer from './assets/denim-pioneer.jpg';

export const DUMMY_PRODUCTS = [
  {
    id: 'p1',
    image: mochaOvercoat,
    title: 'Majestic Vintage Mocha Overcoat',
    price: 129.99,
    description:
      'Channel timeless sophistication with this stunning mocha overcoat. Crafted for the discerning gentleman who appreciates the fine blend of vintage charm and modern elegance.',
  },
  {
    id: 'p2',
    image: dreamGown,
    title: 'Enchanting Blush Dream Gown',
    price: 189.99,
    description:
      'Bask in the glow of elegance with our Enchanting Blush Dream Gown. Embody the regality of a queen with a sweet touch of pink that whispers enchantment. This is the perfect piece for those seeking to create unforgettable moments.',
  },

  {
    id: 'p3',
    image: rainJacket,
    title: 'Vintage Sunshine Rain Jacket',
    price: 49.99,
    description:
      'Brace the showers in style! Our Vintage Sunshine Rain Jacket ensures that you stand out, even in the dullest weather. Because rain is never a reason to compromise on your fashion quotient.',
  },
  {
    id: 'p4',
    image: merlotSuit,
    title: 'Classic Merlot Business Suit',
    price: 249.99,
    description:
    'Step into the boardroom with unmatched confidence in our Classic Merlot Business Suit. Exuding an air of refined class and understated power, it is ideal for the modern executive who values tradition and elegance.',
    },
    {
    id: 'p5',
    image: moonlightDress,
    title: 'Ethereal Moonlight Evening Dress',
    price: 159.99,
    description:
    'Sweep the room off its feet in our Ethereal Moonlight Evening Dress. Crafted to mimic the allure of the moonlight, this dress is a nod to those who appreciate subtle glamour and a standout silhouette.',
    },
    {
    id: 'p6',
    image: denimPioneer,
    title: 'Pioneer Rugged Denim Jacket',
    price: 79.99,
    description:
    'Our Pioneer Rugged Denim Jacket is a tribute to those who embody the spirit of adventure. Designed with durability and comfort in mind, this jacket is a wardrobe essential for the urban explorer.'
    }
];

```

First, let's open the file of *Shop.jsx* and cut the code below into *App.jsx* file component.

This below codes from *Shop.jsx* component file and cut them
```javascript
        {DUMMY_PRODUCTS.map((product) => (
          <li key={product.id}>
            <Product {...product} onAddToCart={onAddItemToCart} />
          </li>
        ))}
```

paste in *App.jsx*, in tag of <Shop
```javascript
  return (
    <>
      <Header
        cart={shoppingCart}
        onUpdateCartItemQuantity={handleUpdateCartItemQuantity}
      />
      <Shop onAddItemToCart={handleAddItemToCart}>
        {DUMMY_PRODUCTS.map((product) => (
          <li key={product.id}>
            <Product {...product} onAddToCart={onAddItemToCart} />
          </li>
        ))}
      </Shop>
    </>
  );
```

and also import the DUMMY and the Product.jsx on *App.jsx* component

```javascript
import Product from './components/Product.jsx';
import { DUMMY_PRODUCTS } from './dummy-products.js';
```

afterward we can replace on tag of Shop in App.jsx from onAddToCart={onAddItemToCart} into onAddToCart={handleAddItemToCart} and also deleting onAddItemToCart={handleAddItemToCart} in the tag Shop

```javascript
import { useState } from 'react';

import Header from './components/Header.jsx';
import Shop from './components/Shop.jsx';
import { DUMMY_PRODUCTS } from './dummy-products.js';

function App() {
  const [shoppingCart, setShoppingCart] = useState({
    items: [],
  });

  function handleAddItemToCart(id) {
    setShoppingCart((prevShoppingCart) => {
      const updatedItems = [...prevShoppingCart.items];

      const existingCartItemIndex = updatedItems.findIndex(
        (cartItem) => cartItem.id === id
      );
      const existingCartItem = updatedItems[existingCartItemIndex];

      if (existingCartItem) {
        const updatedItem = {
          ...existingCartItem,
          quantity: existingCartItem.quantity + 1,
        };
        updatedItems[existingCartItemIndex] = updatedItem;
      } else {
        const product = DUMMY_PRODUCTS.find((product) => product.id === id);
        updatedItems.push({
          id: id,
          name: product.title,
          price: product.price,
          quantity: 1,
        });
      }

      return {
        items: updatedItems,
      };
    });
  }

  function handleUpdateCartItemQuantity(productId, amount) {
    setShoppingCart((prevShoppingCart) => {
      const updatedItems = [...prevShoppingCart.items];
      const updatedItemIndex = updatedItems.findIndex(
        (item) => item.id === productId
      );

      const updatedItem = {
        ...updatedItems[updatedItemIndex],
      };

      updatedItem.quantity += amount;

      if (updatedItem.quantity <= 0) {
        updatedItems.splice(updatedItemIndex, 1);
      } else {
        updatedItems[updatedItemIndex] = updatedItem;
      }

      return {
        items: updatedItems,
      };
    });
  }

  return (
    <>
      <Header
        cart={shoppingCart}
        onUpdateCartItemQuantity={handleUpdateCartItemQuantity}
      />
      <Shop>
        {DUMMY_PRODUCTS.map((product) => (
          <li key={product.id}>
            <Product {...product} onAddToCart={handleAddItemToCart} />
          </li>
        ))}
      </Shop>
    </>
  );
}

export default App;

```

So we replace the props on function of export default function Shop({ onAddItemToCart }) into props {children}

```javascript
import { DUMMY_PRODUCTS } from '../dummy-products.js';
import Product from './Product.jsx';

export default function Shop({ children }) {
  return (
    <section id="shop">
      <h2>Elegant Clothing For Everyone</h2>

      <ul id="products">{children}</ul>
    </section>
  );
}

```

Both files here updated :

```javascript
import { useState } from 'react';

import Header from './components/Header.jsx';
import Shop from './components/Shop.jsx';
import Product from './components/Product.jsx';
import { DUMMY_PRODUCTS } from './dummy-products.js';

function App() {
  const [shoppingCart, setShoppingCart] = useState({
    items: [],
  });

  function handleAddItemToCart(id) {
    setShoppingCart((prevShoppingCart) => {
      const updatedItems = [...prevShoppingCart.items];

      const existingCartItemIndex = updatedItems.findIndex(
        (cartItem) => cartItem.id === id
      );
      const existingCartItem = updatedItems[existingCartItemIndex];

      if (existingCartItem) {
        const updatedItem = {
          ...existingCartItem,
          quantity: existingCartItem.quantity + 1,
        };
        updatedItems[existingCartItemIndex] = updatedItem;
      } else {
        const product = DUMMY_PRODUCTS.find((product) => product.id === id);
        updatedItems.push({
          id: id,
          name: product.title,
          price: product.price,
          quantity: 1,
        });
      }

      return {
        items: updatedItems,
      };
    });
  }

  function handleUpdateCartItemQuantity(productId, amount) {
    setShoppingCart((prevShoppingCart) => {
      const updatedItems = [...prevShoppingCart.items];
      const updatedItemIndex = updatedItems.findIndex(
        (item) => item.id === productId
      );

      const updatedItem = {
        ...updatedItems[updatedItemIndex],
      };

      updatedItem.quantity += amount;

      if (updatedItem.quantity <= 0) {
        updatedItems.splice(updatedItemIndex, 1);
      } else {
        updatedItems[updatedItemIndex] = updatedItem;
      }

      return {
        items: updatedItems,
      };
    });
  }

  return (
    <>
      <Header
        cart={shoppingCart}
        onUpdateCartItemQuantity={handleUpdateCartItemQuantity}
      />
      <Shop>
        {DUMMY_PRODUCTS.map((product) => (
          <li key={product.id}>
            <Product {...product} onAddToCart={handleAddItemToCart} />
          </li>
        ))}
      </Shop>
    </>
  );
}

export default App;

```

*Shop.jsx*

```javascript
import { DUMMY_PRODUCTS } from '../dummy-products.js';
import Product from './Product.jsx';

export default function Shop({ children }) {
  return (
    <section id="shop">
      <h2>Elegant Clothing For Everyone</h2>

      <ul id="products">{children}</ul>
    </section>
  );
}

```

</details>

<details>
<summary>Introducing the Context API</summary>
</details>