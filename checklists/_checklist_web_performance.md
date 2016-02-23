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

