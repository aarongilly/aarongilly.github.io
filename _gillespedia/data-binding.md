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
    
Before I get started, I didn't go to school for any of this. I feel like I'm still very much an amateur. That said,
I'm an amateur who's been doing this sort of stuff as a hobby[^1] for 10 years now. So I guess I
should give myself some modicum of credit.

## What is Data Binding?

When coding you're typically working on either the **front** end of an application *(a.k.a. the part
that users see)*, or the **back** end *(a.k.a. the parts that users don't see that make everything
work)*. 

In terms of web development, the front end is made up of HTML elements like the paragraph element
*("`<p>`")*, inputs *("`<input>`")*, or any of the [other dozen+ types of elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element").
Meanwhile, the back end is made up of, well, data. The back end is concerned with things like variables and
objects. Data binding is a means to keep them synchronized.

![data-binding doodle](https://aarongilly.com/assets/images/logo-small.PNG)

## Benefits of Data Binding

Most of the benefits of data binding are fairly obvious, but here's a list anyway!
- You can focus more on developing the back end, and less on worrying about the logic that keeps the front end up-to-date.
- Because the UI updating takes care of itself, applications become more scalable.
- Enables you to think about the application in terms of the "state" of a (series of) variable(s). 
This opens you up to things like state management, and the ability to implement "undo" and
"redo" logic across the entire application.
- Enables re-usability by maintaining a better separation of concerns. The front end takes care of itself.

## How to Bind Elements to Data

Somewhat surprisingly, it is **not** a trivial task keeping the front end and the back end in sync with
one-another. It's easy to set the text content of an element equal to the value of a variable. It's similarly easy to set a variable based on the value
of some input element. But maintain that relationship over time is difficult. ***Especially*** if there are multiple sources that may update the variable.
Handling these uses cases is a not-so-small part of the reason why many JavaScript frameworks exist.

### The "Easy Way"

Utilize a framework like [React](https://reactjs.org/), [Vue](https://vuejs.org/), [Angular](https://angular.io/), or [Svelte](https://svelte.dev/), 
just to name a few.

### The Manual Way

But you don't **need** a framework for data binding. Implementing it yourself is a good way to "get it". That's what the rest of this article is about.

# Example Implementation of Custom Data Binding

## Live Example

Below are two inputs and a div. All three of which reflect a variable called `observedString`{:javascript}.
You can update the value of `observedString`{:javascript} either input box, and its current value will propagate to all 3 locations.

<html>
    <div style="border: solid; padding: 20px;">
    <div style="display: block">
        <label for="in-one">Input One</label>
        <input id="in-one" type="text" />
    </div>
    <div style="display: block">
        <label for="in-two">Input Two</label>
        <input id="in-two" type="text" />
    </div>
    <div style="display: block">
        <label for="synced-read-only">Variable Value:</label>
        <div id="synced-read-only" style="background-color: lightgrey"></div>
    </div>
    </div>
</html>
  
## Annotated Code

This is what's driving the live example above.

~~~ javascript
<script>
    //CUSTOM OBSERVABLE
    class ObservableString {
        constructor() {
            this._subscribers = [];
            this._value = ""; //initially blank
        }
        addSubscriber(observer) {
            this._subscribers.push(observer);
            return this._subscribers.length;
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
    //CUSTOM OBSERVER
    class ObservingElement {
        constructor(boundElement, observableToWatch) {
            this._element = boundElement;
            observableToWatch.addSubscriber(this);
            this._element.textContent = observableToWatch.get();            
        };
        getElement() {
            return this._element;
        };
        handleChange(newValue) {
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

</script>
~~~


<script>
    //CUSTOM OBSERVABLE
    class ObservableString {
        constructor() {
            this._subscribers = [];
            this._value = ""; //initially blank
        }
        addSubscriber(observer) {
            this._subscribers.push(observer);
            return this._subscribers.length;
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
    //CUSTOM OBSERVER
    class ObservingElement {
        constructor(boundElement, observableToWatch) {
            this._element = boundElement;
            observableToWatch.addSubscriber(this);
            this._element.textContent = observableToWatch.get();            
        };
        getElement() {
            return this._element;
        };
        handleChange(newValue) {
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

</script>

[^1]: ...and sometimes work, when I can