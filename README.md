# react-basics-advanced-concepts
These are Sarthak's go to notes on React.js.

## JSX

JSX stands for JavaScript eXtension i.e. JSX. Think of it as a template language (like blaze, razor syntax etc) but with full power of JavaScript.

- JSX uses camelCase naming convention instead of HTML attribute name i.e.
  - class becomes className
  - tabindex becomes tabIndex
- Making use of curly braces, one can write valid JavaScript inside them.
  - ` <h1>{ 2 + 2 }</h1> ` Here the output will be 4
  - One should either use quotes (for string values) or curly braces (for expressions), but not both in the same attribute.
  - JSX prevents injection attacks
    - By default, React DOM escapes any values embedded in JSX before rendering them. Thus it ensures that you can never inject anything that’s not explicitly written in your application. 
    - Everything is converted to a string before being rendered. This helps prevent XSS (cross-site-scripting) attacks.
    
## Elements

Elements are the smallest building blocks of a React project. 
- Do not get confused between elements and components. Components are made up of elements.
- React elements are immutable. They can only be changed if the component re-renders.
- Rendering react elements only updates the node where the content is changed.
> In our experience, thinking about how the UI should look at any given moment rather than how to change it over time eliminates a whole class of bugs. - React Team

## Components

Conceptually, components are like JavaScript functions. They accept arbitrary inputs (called “props”) and return React elements describing what should appear on the screen.

- Components can beclass based and functional components.
- Always start component name with Capital letter i.e. `<Welcome />`
  - As, react treats components starting with lowercase letters as DOM tags.
    - For example, <div /> represents an HTML div tag, but <Welcome /> represents a component and requires Welcome to be in scope.
- Always name props from the components pointof view and not the context. 
  - We have Comment component which resides in AuthorInfo component, so instead of naming the props name like author use a name like user.
  ``` 
    <AuthorInfo>
      <Comment author={author}>
    </AuthorInfo> 
    
    <AuthorInfo>
      <Comment user={author}>
    </AuthorInfo> 
  ```
- Props are read-only
  - All React components must act like pure functions with respect to their props (Pure functions nver change their inputs and always return same results for their inputs.)
  - State allows React components to change their outputs without affecting the above menthoined rule.
  
## State and Lifecycle
State is similar to props, but it is private and fully controlled by the component.

- Always initialize state in the constructor using `this.state = //State value`
```
//Wrong way
state = {
  name: 'Sam',
  age: '24'
}

//Right way
constructor(props){
  super(props)
  this.state = {
    name: 'Sam',
    age: '24'
  }
}
```
- Class components should always call the base constructor with props. (Refer the above constructor code)
- The componentDidMount() method runs after the component output has been rendered to the DOM. It's good place to make HTTP calls.
- The componentWillUnmount() method runs when the DOM produced by the component is removed. It's a good place to free up resources i.e. like timers etc.
- Update state only using `setState({ value: value })` method. `this.state = value` is wrong way of updating state. The later will not re-render the component, hence the DOM output of the component will remain inconsistent with the state.
- State updates are done asynchronously 
  - React may batch multiple setState() calls into a single update for performance.
  - Because this.props and this.state may be updated asynchronously, you should not rely on their values for calculating the next state.
  ```
  // Wrong
  this.setState({
  counter: this.state.counter + this.props.increment,
  });
  ```
  - To fix it, use a second form of setState() that accepts a function rather than an object. That function will receive the previous state as the first argument, and the props at the time the update is applied as the second argument:
  ```
  // Correct
  this.setState((state, props) => ({
    counter: state.counter + props.increment
  }));
  ```
- React merges the states and the merging is shallow i.e. only the variable updates made to the state will changed, rest of the state variables will remain as is.

  
  

