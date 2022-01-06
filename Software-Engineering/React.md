# React
#📥 
%%
#topic
#concept

**Related:**
-  [[MobX]]
- [[Javascript]]

%%


## Testing

| Tool                  | Usage                                                          |
| --------------------- | -------------------------------------------------------------- |
| react-testing-library | Querying for elements, simulating events or user interactions. |
| Jest and jest-dom     | Making assertions about the element                                                               |

### Jest
Jest is used for React/[[Javascript]] unit testing. Another tool will be needed for integration tests. 
It uses Node, so not a real browser.

Run `npm test` to start in watch mode. By default, only tests files that have changed since last commit. Can press `a` to force it to test all files

```JS
import sum from './sum';

it('sums numbers', () => {  
	expect(sum(1, 2)).toEqual(3);  
	expect(sum(2, 2)).toEqual(4);
});
```


Coverage report: `npm test -- --coverage` *This runs slower than normal tests* 


You can also use [`jest.fn()` and `expect(fn).toBeCalled()`](https://jestjs.io/docs/en/expect.html#tohavebeencalled) to create “spies” or mock functions.

### React-testing-library
react-testing-library is more suited for integration tests and works more directly with dom nodes.

#### Queries 
- Can use async APIs to wait for changes with `waitFor` or `findBy` queries. To find elements within another, use `within` ex: 
```JS
const messages = document.getElementById('messages')
const helloMessage = within(messages).getByText('hello')
```
- Use `getByRole` first to make sure that the app is accessible. Can use `name` option to filter by their accessible name. ex: `getByRole('button', {name: /submit/i})`
