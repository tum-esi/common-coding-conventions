### JavaScript Specific Advice 


#### Creating Namespaces

Functions that do not belong to a class should still be encapsulated into namespaces.

```javascript
const car = {
  start: () => { console.log('start'); },
  stop: ()  => { console.log('stop');  },
}
```



#### Naming Pitfalls

* Never use `e` as variable name, it is too ambiguous. For local short names use
 	* `el` for elements
 	* `ev` for events
 	* `ex` for exceptions
 	* `err` for error


#### Event Handling

 * Use `el.addEventHandler('mousedown', fun)` instead of assigning `el.onmousedown = fun`.



#### Performance

While you should not optimize while writing the initial code, JavaScript is often the bottleneck in web applications.


* **Reduce the complexity of your selectors.** Selector complexity can take more than 50% of the time needed to calculate the styles for an element, compared to the rest of the work which is constructing the style itself.

* **Use local variables.** JavaScript first searches to see if a variable exists locally, then searches progressively in higher levels of scope until global variables. Saving variables in a local scope allows JavaScript to access them much faster.

* **Batching the DOM changes** Batch up DOM transformations to prevent recurring screen renderings. When creating style changes, make all the alterations at once instead of applying changes to each style individually. Furthermore, make style changes to a few elements directly rather than invalidating the page as a whole.

* Avoid `setTimeout` or `setInterval` for visual updates; always use `requestAnimationFrame` instead.

* Move long-running JavaScript off the main thread to Web Workers.



#### References

* https://blog.sessionstack.com/how-javascript-works-the-rendering-engine-and-tips-to-optimize-its-performance-7b95553baeda
* https://developers.google.com/web/fundamentals/performance/rendering/


