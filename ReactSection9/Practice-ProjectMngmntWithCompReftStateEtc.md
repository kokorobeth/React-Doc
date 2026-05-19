<details>
<summary>Module Introduction & Starting Project</summary>

**Practice Project : Advanced Concepts**

*Working with Components, State, Styling, Refs, & Portals*

- Build a "Project Management" Web App
- Build, Style, Configure, & Re-Use *Components*
- Manage State
- Access DOM Elements & Browsers APIs with *Refs*
- Manage JSX Rendering Positions with *Portals*

Now it's time to add some configuration by **npm install** 

```javascript
user@aziz MINGW64 /d/course/udemy/react/Section9/01-starting-project
$ npm install
npm warn deprecated inflight@1.0.6: This module is not supported, and leaks memory. Do not use it. Check out lru-cache if you want a good and tested way to coalesce async requests by a key value, which is much more comprehensive and powerful.
npm warn deprecated @humanwhocodes/config-array@0.13.0: Use @eslint/config-array instead
npm warn deprecated rimraf@3.0.2: Rimraf versions prior to v4 are no longer supported
npm warn deprecated glob@7.2.3: Old versions of glob are not supported, and contain widely publicized security vulnerabilities, which have been fixed in the current version. Please update. Support for old versions may be purchased (at exorbitant rates) by contacting i@izs.me
npm warn deprecated @humanwhocodes/object-schema@2.0.3: Use @eslint/object-schema instead
npm warn deprecated eslint@8.57.1: This version is no longer supported. Please see https://eslint.org/version-support for other options.

added 327 packages, and audited 328 packages in 23s

124 packages are looking for funding
  run `npm fund` for details

2 moderate severity vulnerabilities

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
```

</details>

<details>
<summary>Adding a "Projects Sidebar" Component</summary>

In this section we would like to create folder called **components**. And create new file called *ProjectsSidebar.jsx* and the codes are :

```javascript
export default function ProjectsSidebar() {
    return (
        <aside>
            <h2>Your Project</h2>
            <div>
                <button>
                    + Add Project
                </button>
            </div>
            <ul>

            </ul>
        </aside>
    );
}

```

Also in *App.jsx* file we can modify the codes into :

```javascript
import ProjectsSidebar from "./components/ProjectsSidebar.jsx";

function App() {
  return (
    <main>
      <ProjectsSidebar />
    </main>
  );
}

export default App;

```

When we run and see on the browser, the style is still plan. 

And in the next lecture we are going to style it.

</details>

<details>
<summary>Styling the Sidebar & Button with Talwind CSS</summary>

In **App.jsx** and **ProjectsSidebar.jsx** file we add Talwind CSS

```javascript
import ProjectsSidebar from "./components/ProjectsSidebar.jsx";

function App() {
  return (
    <main className="h-screen my-8 ">
      <ProjectsSidebar />
    </main>
  );
}

export default App;

```

```javascript
export default function ProjectsSidebar() {
    return (
        <aside className="w-1/3 px-8 py-16 bg-stone-900 text-stone-50 md:w-72 rounded-r-xl">
            <h2 className="mb-8 font-bold uppercase md:text-xl text-stone-200">Your Project</h2>
            <div>
                <button className="px-4 py-2 text-xs md:text-base rounded-md bg-stone-700 text-stone-400 hover:bg-stone-600 hover:text-stone-100">
                    + Add Project
                </button>
            </div>
            <ul>

            </ul>
        </aside>
    );
}

```

So we run this **npm run dev**, we'll see the result is nicer than before

![alt text](image.png)

</details>