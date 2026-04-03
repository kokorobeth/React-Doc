# Module Introduction
## React Essentials Deep Dive
**Beyond The Basics**
- Behind the scenes of JSX
- Structuring **Components** and **State**
- **Advanced State** Usage
- **Patterns & Best Practices**

# You Don't Have To Use JSX!
In previous section (section 3) on file of index.jsx we should edit the of react import from the code :
``` import ReactDOM from 'react-dom/client';
import App from './App';
import './index.css';

const entryPoint = document.getElementById("root");
ReactDOM.createRoot(entryPoint).render(<App />);
