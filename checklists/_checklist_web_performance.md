# Web Performance

- Is 'async' flag is being used for script elements that doesn't need to be async?
  - Adding the async keyword to the script tag tells the browser that it should not block the DOM construction while it waits for the script to become available - this is a huge performance win!
  - [Web Fundamentals by Google](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript?hl=en)

- Do you have long running JS in initialization?
  - Long running JS blocks the browser from constructing the DOM, CSSOM and rendering the page. As a result any initialization logic and functionality that is non-essential for the first render should be deferred until later. If a long initialization sequence needs to be run, consider splitting it into several stages to allow the browser to prcess other events in between
  - [Web Fundamentals by Google](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/page-speed-rules-and-recommendations?hl=en)

- Is your CSS in the document head?
  - All CSS resources should be specified as early as possible within the HTML document such that the browser can discover the <link> tags and dispatch the request for the CSS as soon as possible.
  - [Web Fundamentals by Google](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/page-speed-rules-and-recommendations?hl=en)

- Are you avoiding CSS imports? (Preprocessors excluded)
  - CSS import (@import) directive enables one stylesheet to import rules from another stylesheet file. However, these directives should be avoided because they introduce additional roundtrips into the critical path: the imported CSS resources are discovered only after the CSS stylesheet with the @import rule itself has been received and parsed.
  - [Web Fundamentals by Google](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/page-speed-rules-and-recommendations?hl=en)

- Is your Critical Path CSS inlined?
  - For best performance, you may want to consider inlining the critical CSS directly into the HTML document. This eliminates additional roundtrips in the critical path and if done correctly can be used to deliver a “one roundtrip” critical path length where only the HTML is a blocking resource.
  - [Web Fundamentals by Google](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/page-speed-rules-and-recommendations?hl=en)

- Are you trying to have your animations mostly consist of opacity and transforms?
  - Opacity and Tranform are the only two properties which canbe handled by compositor alone. This means that they don't trigger a reflow and a paint. But you need to promote the elements you plan to animate to their own layer (within reason - don’t over do it) by adding the statement: `will-change: transform;`
  - [Web Fundamentals by Google](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count)

- Are you promoting the elements that you plan to animate to their own layer?
  - Promoting elements that you plan to animate by using the statement `will-change: transform` or `will-change:opacity` signals to the browser that changes are incoming and helps the browser to make certain provisions such as creating compositor layers. Though this can cause too much load on memory so shouldn't be performed on unnecessary elements. Like with a '*' selector.
  - [Web Fundamentals by Google](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count)

- Are you using requestAnimationFrame for visual updates instead of setTimeout or setInterval?
  - Avoid setTimeout or setInterval for visual updates. Always use requestAnimationFrame instead. The requestAnimationFrame ensures that the function that is passed as a callback to it will be executed right at the start of the frame which is the right time for visual changes to happen. 
  - [Web Fundamentals by Google](https://developers.google.com/web/fundamentals/performance/rendering/optimize-javascript-execution?hl=en)

- Are you using jQuery's animate method? If so, is it patched to use `requestAnimationFrame` instead of `setTimeout`?
  - Surprisingly jQuery’s default animate behaviour uses ‘setTimeout’. It is advisable to patch it.
  - [Web Fundamentals by Google](https://developers.google.com/web/fundamentals/performance/rendering/optimize-javascript-execution?hl=en)

- Is your heavy, pure computational work (that doesn't require DOM access) running on Web Workers?
  - Since JS runs on the browsers main thread it might block other operations. You can move pure computational work to Web Workers if it doesn’t require DOM access. 
  - [Web Fundamentals by Google](https://developers.google.com/web/fundamentals/performance/rendering/optimize-javascript-execution?hl=en)

- Are your CSS selectors simple?
  - Matching elements to CSS selectors is a big part of the style calculations. Prefer simple selectors (like BEM which has a specific scope) to optimize the process
  - [Web Fundamentals by Google](https://developers.google.com/web/fundamentals/performance/rendering/reduce-the-scope-and-complexity-of-style-calculations?hl=en)
