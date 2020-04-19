# Exam 2 Questions

* Answers should be roughly 2-5 sentences, and in your own words.  
* Some questions ask for a code sample - keep them short and to the point.
* Be sure to be clear - be careful not to use vague pronouns like "it" if I can't be completely sure what "it" is.
* I cannot assume knowledge you don't demonstrate, so be clear and explicit.

## Q1: The first rule I've given about REST services is that the URL should represent a resource.  What does that mean?  Give an example where a url DOES not represent a resource, then describe how to modify it so that it does.
The target of an HTTP request is called a "resource", it can be a document, a photo, or anything else. Each resource is identified by a Uniform Resource Identifier (URI) used throughout HTTP for identifying resources.
Url example which not represent a resource: http://api.example.com/addStudents
In this example, addStudents is an action, we should change it to the target of action
Modified url: http://api.example.com/students

## Q2: If the service returns the username as a plain text string, what is wrong with the below and what would fix it? (Assume the service works without error)
```
  const username = fetch('/username');
  console.log(`user is named ${username}`);
```  
The above code is missing a response object. Fetch returns a promise and the promise resolves with a response object. However, in the above code, the response object doesn't have the parsed body, so we should also call the method to parse the body.
I think we can fix code as the following:

const username = fetch(' /username ');
username.then(response =>  response.text())
.then(username => console.log(`user is name ${username}`);

## Q3: What does it mean to "store your state in the DOM"?  Why shouldn't you do this?
"Store state in the DOM" means using DOM to store and get the data and the state of the variables. In this way, you have the data and the dom element directly related.
The DOM is supposed to be a view of data. The properties of DOM elements should be metadata for the elements themselves, not data from the model. We should better not store state in the dom  because if we store state in the dom, when the view has been changed, the state of the data could also be changed.

## Q4: Explain the differences between a multiple-page-web application and single-page-web application.  Be sure to fully demonstrate your understanding.
Multiple-page-web application is a more traditional web application which consist of several pages. It reloads the entire page and displays the new one when users interact with the web application. Each time when data is exchanged back and forth, a new page is requested from the server to display in a web browser, so multiple-page-web is frontend and backend coupled.
Single-page-web application is a web application which consist of only one single page, it loads all the contents on just a single page instead of navigating the user to different pages, so we don’t use redirect in single-page-web. Also, after the initial page loads, only data is sent back and forth instead of the entire HTML.

## Q5: What is Progressive Enhancement?  What is the difference in an SPA that uses Progressive Enhancement compared to an SPA that doesn't use Progressive Enhancement?
Progressive enhancement is a strategy for web design which emphasizes core webpage content first, then progressively adds more nuanced and technically rigorous layers of presentation and features on top of the content as user's browser/internet connection allow. 
In spa, we can use it for form validation before submit, autocomplete,form submission hijacking, pulling in functionality from other pages…so we can prevent empty input for sumission
The benefit of the strategy is that it allows people to access the basic content and functionality of a web page, while also providing an enhanced version of the page to those with more advanced browser software or bandwidth.

## Q6: Explain how a REST service is or is not similar to a dynamic asset.
A rest service and a dynamic assest are all interact with clients and server.
A dynamic assest doesn’t exist as a file, it’s generated in response to the request. It keeps changing due to users’ different requests.
Rest service is a way to access resources which lie in a particular environment. Data and functionality are considered resources and are accessed using Uniform Resource Identifiers (URIs).  Clients and servers exchange representations of resources by using a standardized interface and protocol.GET, POST, DELETE and PUT are the four common methods that people used to interact with resources.


## Q7: Give an example of a piece of information you should not store in a cookie, and why you should not store it that way.
Anything that should remain secure shouldn’t be stored in a cookie. For example, we should not store credit card numbers in a cookie. Cookies are messages that web servers pass to your web browser when you visit Internet sites. Your browser stores each message in a small file，potentially accessible to anyone. If someone or some application hacked, they can read and edit it, and will make you face much bigger security issue.

## Q8: Explain why it is useful to separate a function that fetches data from the what you do with that data
Separate can make a function not too “coupled” with the rest of code, so changing one part will not mean you have to change everywhere, it makes editing code easier and make code more readable.Function will be more reusable for different purposes.
Function no longer touches any html, and will not change if html changes. If it is given data, it returns data and errors also rejected as data. All changes to html in the event handler will not in the servers call.

## Q9: Explain why try/catch is useless when dealing with asynchronous errors (assume you aren't using async/await)
The reason why try/catch is useless is because try/catch is synchronous. If the error is thrown in asynchronous code, you’ll already completed the try/catch. It doesn’t know it’s inside the try/catch because it’s already run. When try runs, it check for any error and will not find any error, then it’s done and will run the other code outside the try/catch. Catch callback only run when the previous promise resolved or rejected

## Q10: Is separation of concerns a front end issue, a server-side issue, or both?  Describe an example the demonstrates your answer.
I think separation of concerns is both a front end issue and a server-side issue. 
It is a design principle for separating s computer program into distinct sections that each section should only be responsible for a separate thing and should not contain code that deals with other things.
For example, we separate the code into different functions and each function only be responsible for one thing.


## Exam 3 Questions
Answers should be roughly 2-5 sentences, and in your own words.
Some questions ask for a code sample - keep them short and to the point.
Be sure to be clear - be careful not to use vague pronouns like "it" if I can't be completely sure what "it" is.
I cannot assume knowledge you don't demonstrate, so be clear and explicit.
NOTE: Because there is no coding portion to Exam 3, each of these questions is worth more to your grade than the questions on previous Exams! Be sure to have answers you are confident shows your understanding!
## Q1: I have said that React JSX components are like functions and follow many of the same best practices. Give at least 2 such best practices that are good for both JS functions and JSX Components. (Be substantive!)
```
Function TodoList() {
  Const todos = [‘finish homework’, ‘clean room’,’buy food’];
  Return (
   <ul>
      {todos.map((item)

Example1:
<MyComp name=''Bob"/>
Function MyComp(props) {
  Return (<div>{props.name}</div>);
}

Function App() {
  Const stuff = ( <p>This is a secret stuff</p> );
  Return (
    <div>{stuff}</div>
  );
}

Example2:
Import React from 'react';
Const Counter = ({count, changeCount}) => {
  return ( 
    <div>
       <button onClick={ () => changeCount(count-1)}>-</button>
       {count}
       <button onClick={ () => changeCount(count+1)}>+</button>
    </div>
    );
};
Export default Counter;

Import React, {useState} from 'react';
Import Counter from './Counter';

Function CountApp() {
const[count,setCount] = useState(1);
Return (
   <div className=''CountApp''>
      <Counter count={count} changeCount={(newCount) => setCount(newCount)}/>
  </div>
);
}

Example3:
Import React from 'react';
Const Greet = function({greeting}){
    return(
                <p><span>{greeting}</span> Class</p>
             );
};
Export default Greet;

Import React, {useState} from 'react';
Import Greet from './Greet';

Function App() {
    Const [greeting, setGreeting] = useState('hi');
    Return (
                <div>
                     <Greet greeting={greeting}/>
                     <button onClick={ () => setGreeting('Hello') }>Change</button>
                 </div>
            );
}

Example4:
Import React, {useState } from 'react';
Const Counter = ({start}) => {
    Const [count, setCount] = useState(start);
    return ( 
         <button onClick={ () => setCount(count+1)}>{count}</button>
     );
};
Export default Counter;

Import React from 'react';
Import Counter from './Counter';

Function App(){
   Return (
      <Counter start={1}/>
    ):
}

```

      
## Q2: I have said that using Progressive Enhancement (supporting both MPA and SPA) is best, but many places don't do so because of the effort involved. What is at least one major reason not to use SPA alone?(revised to:"What is at least one major reason to use Progressive Enhancement with SPA? (instead of SPA without PE)")
In spa, we can use it for form validation before submit, autocomplete,form submission hijacking, pulling in functionality from other pages…so we can prevent empty input for submission.
SPA remains working when users turn off client-side JS when using Progressive enhancement.
## Q3: The "proxy" setting in your package.json is required for the create-react-app dev server to call a local service, but not if you are calling a service that will always be on a different domain. Explain what happens (in terms of network traffic) when your dev server is running on localhost port 3000 and the page makes a call to /service when you have "proxy" set to http://localhost:4000 and a server running on localhost port 4000 that has the /service service. hint: This should list and describe multiple request/response steps.

Localhost port 3000 is the dev server, localhost port 4000 is services server, they’re on different ports, it usually will cause CORS issues. However, in this scenario, we have “proxy” which can help solve CORS issues.
Anytime the call comes to dev server 3000 that doesn’t exist, it will send to the localhost port 4000 get the result and send them to the page.
On the browser, it can make success calls. The response header will allows  and get response
When we run npm start, hit port 3000 with javaScript code, the server 3000, which is the dev server, doesn’t have /service, but it has the “proxy” configure, so it will send to port 4000 instead, get the response, and send to our request on port 3000. Browser never talks directly to service server. Our code doesn’t know it’s talking to port 4000, because our code is talking to port 3000, the server running on the port 3000 is talking to the server running on the port 4000
## Q4: Follow-up: Using the above scenario, list and describe what the network calls are like after you run npm run build and are only running all of your content on localhost port 4000 when your JSX makes a call to /service
When we run npm run build, we build all the files to static and drop them in one server, doesn’t matter what port it’s on, everything will be on service + static server, all the codes will talk to the exactly same server
## Q5: I have said that you can only pass data "down" in React, not "up". What does that mean? Give simple code sample if that makes it easier to describe.
Components props are often the state of ancestor components. Props can only pass down means if the components have children or descendants, we can assign them props, so it’s passing downward.
Example Code:
```<MyComp name=''Bob"/>
function MyComp(props) {
  Return (<div>{props.name}</div>);
}
```

## Q6: Follow-up: If you can't pass data "up" the component tree, how can anything that is "down" change data? Give simple code samples if that makes it easier to describe.
Descendants can communicate “up” only by using callbacks, and the callbacks pass ancestor down.
Example: 
```
Import React  from 'react';
Const Counter = ({label, onClick}) => {
      return ( 
         <button onClick={onClick }>{label}</button>
     );
};
Export default Counter;

Import React from 'react';
Const Greet = function({greeting}){
    return(
                <p><span>{greeting}</span> Class</p>
             );
};
Export default Greet;

Import React, {useState} from 'react';
Import Greet from './Greet';

Function App() {
    Const [greeting, setGreeting] = useState('hi');
    Return (
        <div>
            <Greet greeting={greeting}/>
            <Counter onClick={ () => setGreeting('Hello') }/>                
        </div>
    );
}
```
1:52
In the above code example, when Counter has to make change, it can’t call setGreeting, all Counter has is onClick, it has no way accessing setGreeting. Counter can call the callback (the highlight part in code example) which Counter’s ancestor passed, but it doesn’t know it’s calling setGreeting. So the ancestor set the callback and pass it down
So the only way Counter can communicate up is by calling a callback

// So the only way Counter can tell its ancestor what happened, its for that the ancestor can pass a callback.
## Q7: Imagine you have a collection of student records, with each having a student id, a name, and an address. (an example of one item in the collection would be: { id: "654321", name: "Bao", address: "123 Main Street" }) Imagine you also have collection of steps to create a pizza, with each step having an ingredient, a quantity, and an instruction. (an example of one item in the collection would be the object { qty: "1 cup", ingredient: "shredded cheese", instructions: "sprinkle over pizza" })
Give a code sample where each collection is shown with at least one more element (2+ students for the first collection, 2+ pizza-making steps). Make sure you make proper use of arrays and objects. Explain why you've chosen each way of making a collection (e.g. Why you use an array for one or both, or why you use an object for one or both)
```
const students = [
  {id: “123456”,
  name:“Bao”,
 Address: “123 Main Street”},
 {id: “123457:,
  name: “Andy”,
Address: “205 Terry Street”},
{id: “123458”,
Name: “Marry”,
Address: “103 N 90st Street”},
]
```
```
const steps = [
{qty: “1 cup”,
Ingredient: “Shredded cheese”,
Instructions: “sprinkle over pizza”},
{qty: “2 cups”,
Ingredient: “Mushroom”,
Instructions: “sprinkle over pizza”},
{qty: “1 cup”,
Ingredient: “Pepperoni”,
Instruction: “sprinkle over pizza”},
]
```
Arrays: Arrays come with several, very useful native methods. We can add a new element to existing array instance using push() and remove the last element from the array via pop(). We can also use splice() to remove n elements and/or insert new element(s) at index i.
Object: Think about objects as associative arrays, i.e. list of key -> value pairs. These keys are referred to as object properties. For collection of steps of making pizza, the object has an ingredient, a quantity, and an instruction. I think it doesn’t have any unique property that can be used as the key, so it’s not suitable to use object to make a collection, so I choose array for steps collection.
 
Arrays: Generally when we work with arrays, we care less about indexes and more about values. One of the common operations we perform with Arrays is checking if a certain value is in the array. This is easily accomplished using indexOf() method.
 
Object: In contrast to Arrays, we generally want to know if an Object contains a certain property. Usually we will write a function that takes Object as an argument and will expect that it contains a certain set of properties. This Object can come from an API or some other piece of code and we shouldn't rely on it having all the properties we expect. It is always a good idea to check whether the property exists before accessing the value behind that property. Objects come with hasOwnProperty() method which allows us to do just that.
 
 
 ## Q8: How does inheritance in JS relate to a prototype? Give a simple code sample if it helps explain.
Is JS, objects can have “inheritance” where an object can use the properties/methods of another object. If the code tries to access a value on the object, and the object doesn’t have it defined for itself, it will check to see if it’s prototype has it. Because the prototype is an object, when asked for this value, if it doesn’t have it, it will check to see if it’s prototype has it. This continues until an object doesn’t have a prototype. 

Code Sample:
```const Cat = function(name) {
      This.name = name;
   };
  Cat.prototype.beNice = function() {
      console.log(`${this.name} says ‘No’ `);
};
const maru = new Cat(‘Maru’);
maru.beNice(); 
```
In the above code, I create  a function, and use the new keyword to call the function to create a new object, and the prototype property is assigned as the prototype of the new object. maru.beNice is inherited, but maru.name is not inherited.


## Q9: What is wrong about this code sample? if( !username || username == undefined) { be sure to explain why that is wrong.

In the above code, `!username` means username is null or undefined, so it already includes the situation `username == undefined`, therefore it’s not necessary to write it again, we can just write `if(!username)`.

## Q10: What is decoupling? What is an example of decoupling in a React app?
Decoupling makes editing code easier and makes code more readable. Component will be more reusable for different purposes.
A component has one reason to change when it implements one responsibility, or simpler when it does one thing.

