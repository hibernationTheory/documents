# Testing For React

## Summary

One of the primary ways of unit testing react components is using a technique called *shallow rendering*. Shallow rendering renders only one level deep into the given object. Meaning the child components would appear with their component names displayed like: `<ChildComponent />` . Having a limited scope like this is beneficial for unit testing.

Shallow rendering outputs a JS object that represents the component. This might not be too useful to work with since you might be writing your code using JSX. In that case you would rather want to see how your test failed in JSX code rather than in JS code. So we can use a JSX extension for our testing (our assertation) library to be able to work directly with the JSX string. In my case I am using *jsx-chai*

It works like this:
```
npm i --save-dev react-addons-test-utils
```

```
import {Simulate, createRenderer, renderIntoDocument} from 'react-addons-test-utils'

let renderer = createRenderer();
renderer.render(<MyComponent />);
let actualElement = renderer.getRenderOutput();
expect(actualElement).to.deep.equal(<My Component/>)
```

But the problem with shallow rendering is that without rendering components to DOM you won't be able to see certain properties of them like state or not be able simulate events on them.

This is where jsdom comes into play. You can mock a DOM api using jsdom in pure javascript which will fool React into thinking that it is rendering into the document using 'renderIntoDocument'. You can also use the 'Simulate' method to simulate events on dom nodes. You can as well use the 'refs' to fetch other elements. I had a problem installing latest version of jsdom though since it was requiring node 4+, I couldn't install an earlier version as well since a dependency called 'contextify' was causing lots of issues. So opted to use a fork of it called 'jsdom-no-contextify'.

## from 'blog.algolia.com'
https://blog.algolia.com/how-we-unit-test-react-components-using-expect-jsx/

"scripts": {
  "test": "mocha test.js --compilers js:babel-core/register",
  "test:watch": "mocha test.js --compilers js:babel-core/register --watch --reporter min"
}

## from 'jaketrent.com'
http://jaketrent.com/post/testing-react-with-jsdom/

- it seems like you can set default options for *mocha* inside a `/test/mocha.opts` file.

```
--require test/utils/dom.js
--require should
--reporter nyan
```

## Related

### jsx-chai-methods

```
expect(<Component/>).to.be.jsx // JSX-CHAI
expect('Component').to.not.be.jsx // JSX-CHAI
expect(<Component/>).to.deep.equal(<Component/>) 
expect(<Component prop='value'/>).to.not.deep.equal(<Component prop='other-value'/>) 
expect(<Component/>).to.eql(<Component/>) 
expect(<Component prop='value'/>).to.not.eql(<Component otherProp='value'/>) 
expect(<Component><h1>Title</h1></Component>).to.include(<h1>Title</h1>) 
expect(<Component><h1>Title</h1></Component>).to.not.include(<div/>)
```

## Resources

- https://facebook.github.io/react/docs/test-utils.html
- http://jaketrent.com/post/testing-react-with-jsdom/
- https://blog.algolia.com/how-we-unit-test-react-components-using-expect-jsx/
- https://discuss.reactjs.org/t/whats-the-prefered-way-to-test-react-js-components/26/26
- http://reactkungfu.com/2015/07/approaches-to-testing-react-components-an-overview/
- https://github.com/robertknight/react-testing
- https://medium.com/@bruderstein/the-missing-piece-to-the-react-testing-puzzle-c51cd30df7a0#.796xbphuq
- http://www.hammerlab.org/2015/02/14/testing-react-web-apps-with-mocha/
- https://www.npmjs.com/package/jsx-chai
- https://blog.algolia.com/modern-javascript-libraries-the-isomorphic-way/
- http://jamesknelson.com/testing-in-es6-with-mocha-and-babel-6/
- https://facebook.github.io/react/docs/test-utils.html
- http://www.newmediacampaigns.com/blog/refactoring-react-components-to-es6-classes
- https://egghead.io/series/react-testing-cookbook
- http://www.newmediacampaigns.com/blog/refactoring-react-components-to-es6-classes


