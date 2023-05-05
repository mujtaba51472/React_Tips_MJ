# useEffect

<p>
`definition :`
useEffect is a hook provided by React that allows functional components to use lifecycle methods and manage side effects. 
It allows you to perform certain actions in response to changes in the component, such as 
`updating the DOM`, `fetching data from an API`, or `subscribing to events`


## Example
```javascript
 useEffect(() => {
   console.log('useEffect runs)
  }, []);
```

The useEffect hook takes two arguments: `a function (callback fun)`that describes what side effect you want to perform, and 
`an optional dependency array  ([])` that specifies when the effect should run. 
The effect function is called after the component has been rendered, and then it can perform whatever action you want.



###  How useEffect runs |  exact flow 
`first` ,
it will be called or run the code or function provided inside just after the component mount for the first time or initial render 
This is when There is no dependency in the array as provide to the useEffect as ; 

```javascript
 useEffect(() => {
   console.log('code runs | function executing etc')
  }, []);
```
component render , useeffect runs and log  `code runs | function executing etc` 
This is similar what we could do in class component of `componentDidMount()`

`Second`
when there is dependency provided in the array

```javascript
 useEffect(() => {
   console.log('code runs | function executing etc')
  }, [dependency1 , dependency2]);
```
Now as from above discussion our component has been already rendered or mounted now 
if there is changing in dependency1 or dependency2 (comparing it pre and new value) , component will be re render once again and useeffect will runs same way , whenever there is changing in dependency(component maybe re rendering) then useEffect will run




##  What we can do with useEffect

Three major benenfits of useeffect
1.`Fetching data from an API:`

```jaavsrvipt
import { useState, useEffect } from 'react';

function MyComponent() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch('https://my-api.com/data')
      .then(response => response.json())
      .then(data => setData(data))
      .catch(error => console.log(error));
  }, []);

  return (
    <div>
      {data.map(item => (
        <div key={item.id}>{item.name}</div>
      ))}
    </div>
  );
}
```

2.` Updating the document title | interacting with DOM:`

```javascript
import { useEffect } from 'react';

function MyComponent() {
  useEffect(() => {
    document.title = 'My Page Title';
  }, []);

  return (
    <div>
      <h1>Hello World</h1>
    </div>
  );
}
```

.` Subscribing to events:`

```javascript
import { useState, useEffect } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const handleResize = () => {
      setCount(window.innerWidth);
    };

    window.addEventListener('resize', handleResize);

    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []);

  return (
    <div>
      <h1>Window Width: {count}px</h1>
    </div>
  );
}
```


##  How useEffect handle The life cycle of the react component
ans:

The useEffect hook is a powerful feature of React that allows functional components to manage their lifecycle and handle side effects. It provides an easy way to execute code in response to changes in the component, such as updates to the state or props.

In terms of the component lifecycle, the useEffect hook can be used to replace several lifecycle methods, such as componentDidMount, componentDidUpdate, and componentWillUnmount, all in a single function.

When a component mounts for the first time, the useEffect hook runs the code inside its callback function. This is similar to how componentDidMount works in class components. After the initial render, the useEffect hook will run again only if there is a change in the dependency array provided as the second argument. This means that the effect will run whenever the component re-renders due to a change in the state or props.

The useEffect hook can also be used to handle cleanup tasks when a component unmounts. This is similar to how componentWillUnmount works in class components. By returning a cleanup function from the effect, you can ensure that any resources used by the effect are cleaned up when the component is removed from the DOM.

Overall, the useEffect hook is a powerful tool for managing the lifecycle of a functional component and handling side effects. It provides an easy way to execute code in response to changes in the component, replace several lifecycle methods in a single function, and handle cleanup tasks when the component is removed from the DOM.



##  Why useEffect after component render | re render 

1. useEffect is designed to run after the component has rendered because it allows you to perform side effects after the browser has painted the initial screen. This is important because performing side effects during the rendering process can block the browser's rendering engine, resulting in a slow and unresponsive user interface.

2By running useEffect after the component has rendered, React ensures that your component's rendering process is fast and efficient, while still allowing you to perform any necessary side effects. This makes it possible to build complex user interfaces that respond quickly and smoothly to user interactions.

3. Additionally, running useEffect after the component has rendered allows you to access and manipulate the component's DOM elements, which may not be available during the initial rendering process. This is useful for setting up event listeners, updating the document title, or performing any other side effect that requires access to the DOM.



##  How useEffect will response here | how setInterval will run 

```javascript
  let i = 5;
  useEffect(() => {
    console.log('useeffect');
    setInterval(() => {
      i++;
      console.log(i); // log the value of i
    }, 1000);
  }, [i]);
```
`explanation`: 
In the code you provided, i is declared and initialized with a value of 5.

Then, a useEffect hook is used with a dependency array containing only i. This means that the effect function will be called after the initial render, and then again whenever the value of i changes.

Inside the effect function, a setInterval function is used to repeatedly increment i and log its value to the console every 1 second.

However, since the dependency array only contains i, and i is not updated using setState or any other mechanism that triggers a re-render, the effect function will only be called once after the initial render, and not again, even though the value of i is changing.

So, in this case, the setInterval function will run continuously and log the incremented value of i to the console, but the useEffect hook will not be called again to log 'useeffect' to the console.



</p>