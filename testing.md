# Front-End JavaScript Testing Strategies

While running tests in Node.js is sufficient for most server-side modules, testing browser code in Node.js is not enough in most cases. We suggest these testing strategies depending on the project type:

| Project Type | Test Types | Runtime |
| --- | --- | --- |
| Library of pure functions without DOM API calls | unit, integration | Node.js |
| Library with DOM API calls | unit, integration | [browsers](browsers.md) |
| Front-end component | unit, integration, functional | [browsers](browsers.md) |
| Application | unit, integration, functional | [browsers](browsers.md) |

This table is subjective and is presented for reference. Adapt the testing strategy for your own needs:

- It's great to test a **library of pure functions** in browsers as well because level of JavaScript support can vary
- If a **library of pure functions** has no dependencies, integration tests are not required
- **Library with DOM API calls** could require functional tests if it adds interactivity to components or a page
- **Front-end component** sometimes doesn't require functional tests, if there is nothing interactive
- Use your good judgment
