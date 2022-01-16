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
I'm an amateur who's been doing this sort of stuff as a hobby and sometimes for work for 10 years now. So I guess I
should give myself some modicum of credit.

# Preamble - What is Data Binding?

When coding you're typically working on either the **front** end of an application (a.k.a. the part
that users see), or the **back** end (a.k.a. the parts that users don't see that make everything
work). In terms of web development, the front end is made up of HTML elements like the paragraph element
*("<p>")*, inputs
*("<input>")*, or any of [of other types of elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element").
Meanwhile, the back end is made up of, well, data. The back end is concerned with things like variables and
objects. Somewhat
surprisingly, it is **not** a trivial task keeping the front end and the back end in sync with
one-another. It's easy to set the text
content of an element equal to the value of a variable. It's similarly easy to set a variable based on the value
of some input element. But
what if there are multiple ways the variable may be updated? This is actually a not-so-small part of the reason
why many JavaScript frameworks
exist.

But you don't **need** to rely on a framework for data binding. And implementing it myself made me
finally "get it".

# Example: Data Binding via Implementation of a Custom-Built Observable Class</h2>

    <input id="in-one" type="text" /><label for="in-one">Input One</label>
    <input id="in-two" type="text" /><label for="in-two">Input Two</label>
    <div id="synced-read-only"></div><label for="synced-read-only">Variable Value</label>

## Benefits of Data Binding

Most of the benefits of data binding are fairly obvious, but here's a list anyway!
- You can focus more on developing the back end, and less on worrying about the logic that keeps the front end up-to-date.
- Because the UI updating takes care of itself, applications become more scalable.
- Enables you to think about the application in terms of the "state" of a (series of) variable(s). 
This opens you up to things like state management, and the ability to implement "undo" and
"redo" logic across the entire application.
- Enables re-usability by maintaining a better separation of concerns. The front end takes care of itself.
  
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