# React.js Conf 2015
## Formatting with FormatJS and react-intl

### Source
https://www.youtube.com/watch?v=Sla-DkvmIHY

### Summary

- Localization is a sibling concept to internationalization
- Formatting aspect of the internationalization involves formatting things based on the locale, context, current time or amount (should something be plural or singular)
- In other languages to deal with this problem yo uhave lots of standart libraries. In JS this is not standardized but still is being tackled by 3rd part libs such as moment.js
- Ecmascript 5.1 has actually some support for internationlization options, Like:
    + Intl.NumberFormat
    + Intl.DateTimeFormat
    + Intl.Collator (sorting strings when you have accents)
- These things even work in browser and node.js supports them too. For cases where it is not supported you can use a polyfill like *Intl.js*
- How there work is:

```
new Intl.NumberFormat().format(1000);
// 1,000
// Checks the locale of your OS and provides the results automatically.

new Intl.DateTimeFormat({
    month: 'long',
    day: 'numberic',
    year: 'numeric'
}).format(Date.now())
// January 28, 2015

```
- The problem is that it is really expensive to create these so you ideally create them once and hold on to it and re-use in your application. 
- The other problem is that this is imperative.

- they built something called react-intl which provides you with react components that allows you to format things in a very declarative way.
    + You are given a component like 'FormattedDate' and you provide it with a value and formatting related props. It renders the desired outcome.

#### String Messages

- There is this way of formatting messages to indicate which parts of the text needs to be formatted in which way. The standard is driven by an international body and is driving the features in other languages as well. It looks like string templates in JS. (ICU message syntax)

```
"Hello, {name}"
"You're {age, number} years old"
```

- One cool thing is that professional translators know this syntax so they can format the text with the information that is provided.

- They have an 'intl' mixin as well which when passed as a mixin to a component would expect a 'locales' prop to be passed and will in turn would propogate the given information to the subchildren in the hierarchy. Or you can proivde an array with a fallback locales as well.

- Format.js is a set of libraries of which React-intl is a part of. Format.js is the big picture though.

- They eventually want to see these codes:
Intl.MessageFormat
Intl.RelativeFormat to be built into JS (javascript runtimes)
