---
title: "Data Binding with Vanilla JavaScript "
excerpt: "Back End meet Front End."
date: "2022-01-16"
categories: 
- "coding"
header:
   teaser: "https://lh3.googleusercontent.com/pw/AM-JKLVT2CciUr6thq3QZO9qLtT48hHZK2tYE8U0t5kYK0-IeOfM-N_dlcZoP7WWrHNwcdGgJfp1QL2uXrmzi1wESExEmxM8y0pPdhaz0cgtBMXpHUeavObgQKdWLwQ0r04P-phoMqGAegRab4in8VBRUjBLHw=w300"
mathjax: true
---
    
Before I get started - I didn't go to school for any of this. I feel like I'm still very much an amateur. That said, I'm an amateur who's been doing this sort of stuff as a hobby[^1] for 10 years now. So I guess I should give myself some modicum of credit.

![data-binding doodle](https://aarongilly.com/assets/images/logo-small.PNG)

## What is Data Binding?

When coding you're typically working on either the **front** end of an application *(a.k.a. the part
that users see)*, or the **back** end *(a.k.a. the parts that users don't see that make everything
work)*. 

In terms of **web development**, the front end is made up of HTML elements like paragraph elements
*("`<p>`")*, divs *("`<div>`")*, inputs *("`<input>`")*, or any of the [other dozen+ types of elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element").
Meanwhile, the back end is concerned with data - things like variables and objects. Data binding is a means to keep the front and back synchronized.

## Live Example

Below are two inputs and a div. All three of which reflect a variable called `observedString`{:javascript}.
You can update the value of `observedString`{:javascript} either input box, and its current value will propagate to all 3 locations.

<html>
    <div style="border: solid; padding: 20px;">
    <div style="display: block">
        <label for="in-one">Input One:</label>
        <input id="in-one" type="text" />
    </div>
    <div style="display: block">
        <label for="in-two">Input Two:</label>
        <input id="in-two" type="text" />
    </div>
    <div style="display: block">
        <label for="synced-read-only">Value of <span style="font-family: monospace; color: darkgrey;">observedString</span>:</label>
        <div id="synced-read-only" style="background-color: lightgrey"></div>
    </div>
    </div>
</html>

## Benefits of Data Binding

Most of the benefits of data binding are fairly obvious, but here's a list anyway!
- You can focus more on developing the back end, making the front end prettier, and worrying less about the logic that keeps them in sync.
- Because the UI updating takes care of itself, applications become more scalable.
- Enables you to think about the application in terms of the "state" of a *(series of)* variable *(s)*. This opens you up to things like state management, and the ability to implement "undo" and "redo" logic across the entire application.
- Enables re-usability by maintaining a better separation of concerns.

## How to Bind Elements to Data

Perhaps somewhat surprisingly, it is **not** a trivial task keeping the front end and the back end in sync with one-another. 

It's easy to set the text content of an element equal to the value of a variable.  
It's similarly easy to set a variable based on the value of some input element.  

But maintaining that relationship over time is difficult. ***Especially*** if there are multiple sources that may update the variable.
Handling these uses cases is a not-so-small part of the reason why many JavaScript frameworks exist.

### The "Easy Way"

Utilize a framework that provides data binding mechanisms, like [React](https://reactjs.org/), [Vue](https://vuejs.org/), [Angular](https://angular.io/), or [Svelte](https://svelte.dev/), 
just to name a few.

### The Manual Way

But you don't **need** a framework for data binding. Implementing it yourself is a good way to "get it". That's what the rest of this article is about.

# Implementation of Custom Data Binding
  
## Annotated Code

This is what's driving the live example above.

### Observable Class

If you want data binding, you don't have the luxury of binding to primative variable types. An "Observable" is one that contains a value, but also maintains a list of subscribed *Observers*. Each time its value is set, the Observerable object takes care of notifying each of the Observers in its list by issuing them a function call passing it the new value. To be an Observer is to be an object that implements the function to be called.

~~~ javascript
class ObservableString {
    constructor() {
        this._subscribers = []; //list of "Observers" watching this value
        this._value = ""; //the value itself
    }
    addSubscriber(observer) {
        //in order to bind to the Observable, an Observer must add itself
        //to a 'subscriber' list that's maintained by the Observable.
        this._subscribers.push(observer); 
    }
    set(newValue) {
        //setter must be used to set the Observed value. This is what
        //lets the Observable know it needs to notify its subscribers
        this._value = newValue;
        this._subscribers.forEach(subscriber => { 
            //in order to be an Observer, you *must* implement a 'handleChange'
            //function on the Observer. 
            //(Note 'handleChange' is just what I called it, really
            //any name works so long as all Observers have it)
            subscriber.handleChange(this._value)
        });
    }
    get() {
        //simple getter. No need to notify anybody that value is being read.
        return this._value;
    }
}
~~~ 

### Observer Class

An Observer is something that implements a function that's called by the Observable each time its value is set. In my case, I've named that function 'handleChange'. For the purposes of data binding, the handleChange function updates the value of a displayed element.

~~~ javascript
class ObservingElement {
    constructor(boundElement, observableToWatch) {
        this._element = boundElement; //the div or input or paragraph element
        observableToWatch.addSubscriber(this); //register this Observer instance with the Observable instance it cares about
        this._element.textContent = observableToWatch.get(); //grab its current value            
    };
    //this is the function the Observable will call each time its value is set.
    handleChange(newValue) {
        //this if sets the visible text on the element, which may be an input
        if(this._element.tagName === "INPUT"){
            this._element.value = newValue;
        }else{
            this._element.textContent = newValue;
        }
    }
}
~~~

### Creating Instances & Subscribing

To bind elements to a data object, you need references to both things. Then you instantiate instances of the Observable & Observer classes.

~~~ javascript
//Obtaining References to Elements
let inOneElement = document.querySelector("#in-one");
let inTwoElement = document.querySelector("#in-two");
let readOnlyElement = document.querySelector("#synced-read-only");

//CREATE CLASS INSTANCES TO HANDLE BINDING
let observedString = new ObservableString();
let one = new ObservingElement(inOneElement,observedString);
let two = new ObservingElement(inTwoElement, observedString);
let three = new ObservingElement(readOnlyElement, observedString);
~~~

### Making Data Binding 2-Way

Up to this point, you have everything you need for one-directional data binding. The elements will reflect the current value of the Observable every time it is set. However it's common that a bound element is *also* a mechanism for updating the Observable. To do that, simply have the elements call the "set" function on the Observable instance.

~~~ javascript
//WIRE INPUTS TO OBSERVABLE STRING
inOneElement.addEventListener("input", ()=> observedString.set(inOneElement.value));
inTwoElement.addEventListener("input", ()=> observedString.set(inTwoElement.value));
~~~

## Whole Code

I get annoyed when I read articles like this and they don't have a section like this. Here you go copy/pasters:

~~~ javascript

/*
This script assumes you have inputs named "in-one" and "in-two" and a div named "synced-read-only". Like so:
<html>
    <div style="border: solid; padding: 20px;">
    <div style="display: block">
        <label for="in-one">Input One:</label>
        <input id="in-one" type="text" />
    </div>
    <div style="display: block">
        <label for="in-two">Input Two:</label>
        <input id="in-two" type="text" />
    </div>
    <div style="display: block">
        <label for="synced-read-only">Value of observedString:</label>
        <div id="synced-read-only" style="background-color: lightgrey"></div>
    </div>
    </div>
</html>
*/

class ObservableString {
    constructor() {
        this._subscribers = []; //list of "Observers" watching this value
        this._value = ""; //the value itself
    }
    addSubscriber(observer) {
        //in order to bind to the Observable, an Observer must add itself
        //to a 'subscriber' list that's maintained by the Observable.
        this._subscribers.push(observer); 
    }
    set(newValue) {
        //setter must be used to set the Observed value. This is what
        //lets the Observable know it needs to notify its subscribers
        this._value = newValue;
        this._subscribers.forEach(subscriber => { 
            //in order to be an Observer, you *must* implement a 'handleChange'
            //function on the Observer. 
            //(Note 'handleChange' is just what I called it, really
            //any name works so long as all Observers have it)
            subscriber.handleChange(this._value)
        });
    }
    get() {
        //simple getter. No need to notify anybody that value is being read.
        return this._value;
    }
}

class ObservingElement {
    constructor(boundElement, observableToWatch) {
        this._element = boundElement; //the div or input or paragraph element
        observableToWatch.addSubscriber(this); //register this Observer instance with the Observable instance it cares about
        this._element.textContent = observableToWatch.get(); //grab its current value            
    };
    //this is the function the Observable will call each time its value is set.
    handleChange(newValue) {
        //this if sets the visible text on the element, which may be an input
        if(this._element.tagName === "INPUT"){
            this._element.value = newValue;
        }else{
            this._element.textContent = newValue;
        }
    }
}

//Obtaining References to Elements
let inOneElement = document.querySelector("#in-one");
let inTwoElement = document.querySelector("#in-two");
let readOnlyElement = document.querySelector("#synced-read-only");

//CREATE CLASS INSTANCES TO HANDLE BINDING
let observedString = new ObservableString();
let one = new ObservingElement(inOneElement,observedString);
let two = new ObservingElement(inTwoElement, observedString);
let three = new ObservingElement(readOnlyElement, observedString);

//WIRE INPUTS TO OBSERVABLE STRING
inOneElement.addEventListener("input", ()=> observedString.set(inOneElement.value));
inTwoElement.addEventListener("input", ()=> observedString.set(inTwoElement.value));
~~~


# What the Live Example Doesn't Do

This is a minimal example. I initially made some bits of it fancier and more complicated, but wound up removing anything that wasn't
strictly for the benefit of making data binding work. Even within that context, though, there are some things I didn't do[^2].

- Lifecycle Management 
    - There is no mechanism in that code snippet to *unsubscribe* an element from the bound string. You can imagine a scenario where you'd want to de-couple an element from its source.
- Asyncronous Support
    - This is an example of the "Observable" pattern. There's another pattern called 
    "pub/sub" that includes a "Broker" in the middle that keeps track of publishing parties and their subscribers. This allows for binding across sources, asycnronous binding, and for bound instances to remain ignorant of each other.
- Validation Logic
    - You could implement an "`maybeSet()`{:javascript}" function that checks the input against some criteria. If the input is valid, it propagates the change. If the input is rejected, it returns an error condition and doesn't propagate.
- State Management
    - Like validation - this is sort of separate from data binding, but made easier by it. You could keep a queue of previous states in the Observable Class. Then implement functions to "undo", "redo", and "go to" specific points in history and your UI would update accordingly.

[^1]: ...and sometimes work, when I can  
[^2]: ...for now


<script>
    class ObservableString {
    constructor() {
        this._subscribers = [];
        this._value = "";
    }
    addSubscriber(observer) {
        this._subscribers.push(observer); 
    }
    set(newValue) {
        this._value = newValue;
        this._subscribers.forEach(subscriber => { 
            subscriber.handleChange(this._value)
        });
    }
    get() {
        return this._value;
    }
}

class ObservingElement {
    constructor(boundElement, observableToWatch) {
        this._element = boundElement;
        observableToWatch.addSubscriber(this);
        this._element.textContent = observableToWatch.get();
    };
    handleChange(newValue) {
        if(this._element.tagName === "INPUT"){
            this._element.value = newValue;
        }else{
            this._element.textContent = newValue;
        }
    }
}

let inOneElement = document.querySelector("#in-one");
let inTwoElement = document.querySelector("#in-two");
let readOnlyElement = document.querySelector("#synced-read-only");

let observedString = new ObservableString();
let one = new ObservingElement(inOneElement,observedString);
let two = new ObservingElement(inTwoElement, observedString);
let three = new ObservingElement(readOnlyElement, observedString);

inOneElement.addEventListener("input", ()=> observedString.set(inOneElement.value));
inTwoElement.addEventListener("input", ()=> observedString.set(inTwoElement.value));
</script>