# Front-End JavaScript Testing Strategies

While running tests in Node.js is sufficient for most server-side modules, testing browser code in Node.js is not enough in most cases. We suggest these testing strategies depending on the project type:

| Project Type | Test Types | Runtime |
| --- | --- | --- |
| Library of pure functions without DOM API calls | unit, integration | Node.js |
| Library with DOM API calls | unit, integration | [browsers](browsers.md) |
| Front-end component | unit, integration, functional | [browsers](browsers.md) |
| Application | unit, integration, functional | [browsers](browsers.md) |
