# Web Performance

- Is 'async' flag is being used for script elements that doesn't need to be async?
  - Adding the async keyword to the script tag tells the browser that it should not block the DOM construction while it waits for the script to become available - this is a huge performance win!
