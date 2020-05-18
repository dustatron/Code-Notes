# React-Router

[Router Docs](https://reacttraining.com/react-router/web/example/basic)  | [Epicodus Lesson](https://www.learnhowtoprogram.com/react/react-with-nosql/react-router)

install react router

```shell
npm install --save react-router-dom@5.1.2
```

Redirecting

https://dev.to/projectescape/programmatic-navigation-in-react-3p1l

1. <Redirect> Component

```javascript
import { Redirect } from "react-router-dom";

state = { redirect: null };
render() {
  if (this.state.redirect) {
    return <Redirect to={this.state.redirect} />
  }
  return(
  // Your Code goes here
  )
}
```

2. useHistory Hook

```javascript
import { useHistory } from "react-router-dom";

function App() {
  let history = useHistory();
}

//use this line in a function
history.push('/someRoute') 
```

StackOverflow // talking about Routing

https://stackoverflow.com/questions/45122800/react-router-switch-behavior

3. Passing params

   ```javascript
   //App.js  
   return (
       <Router>
         <Header onAnimalClick={setAnimal} />
         <Route
           exact
           path="/list/:type"
           component={() => {
             return <AnimalList showAnimal={animal} />;
           }}
         />
   			// These lines are taking params
         <Route path="/detail/:animalId/:type" component={AnimalDetails} />
         <Route path="/edit/:animalId/:type" component={AnimalEdit} />
         <Route path="/add" component={AddAnimal} />
       </Router>
     );
   
   //Passing Params with a link
   <Link to={{ pathname: `/edit/${params.animalId}/${params.type}`}}>
   //`
         <button className='button'>Edit</button>
   </Link>
   
   //AnimalDetails.js
   // using params
   function AnimalDetails(props) {
     const { match: { params } } = props;
     
     //this will supply the value of the param passed in. 
     const typeOfAnimal = params.type;
   }
   ```

   

