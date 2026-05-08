---
Title: A Guide To Jest
Date Created: 06-February-2026
Last Updated: 06-February-2026
Tags:
  - SWE/Testing/TestingLibraries/Jest
---
# Writing A Simple Test Case
---
<b><span style='color: #DDA0DD'>Jest</span></b> uses 2 key words to <b><span style='color: #FFD700'>start a new individual test case</span></b>, they are `test` or `it`.

It takes in 2 arguments:
- The test description
- A function on what the test will do

>[!example] Simple test case
>```js
>test('two plus two is four', () => {
>	expect(2 + 2).toBe(4);
>}); 
> ```

At the end of the test we need an `except` & a `matcher` which is to say <b><span style='color: #FFD700'>result matches expected result</span></b>.

Here are a few <b><span style='color: #DDA0DD'>matchers</span></b>:
- `toBeNull`
- `toBe(value)`
- `toBeTruthy`
- `toContainEqual(item)`
- `toContain(item)`
- `toEqual(value)`
- `toMatchObject(object)`
## Grouping Tests

We can group tests together using the `describe` keyword

>[!example] Example of grouping tests cases
>```js
>describe('my tests', () => {
>	test('two plus two is four', () => {
>		expect(2 + 2).toBe(4);
>	});
>	
>	test('minus one thats three quick mafs', () => {
>		expect(4 - 1).toBe(3);
>	});
>});
>```

## Skipping Tests

We can **skip tests** by using the `.skip`or add the prefix `x` to the `test` function (*so its* `xtest(...)`)

>[!example] Example of grouping tests cases
>```js
>// The xtest is redundant but it shows the 2 ways you can skip a test
>describe.skip('my tests', () => {
>	xtest('two plus two is four', () => {
>		expect(2 + 2).toBe(4);
>	});
>});
>```

>[!question] Why skip tests?
>Maybe you want to focus on a particular module or unit so you do not want the results or logs from the other tests to interfere.

## Order Of Execution

In a test file, <b><span style='color: #DDA0DD'>Jest</span></b> will execute all `describe` statements <b><span style='color: #FFD700'>first</span></b> then the actual `test` will get <b><span style='color: #FFD700'>executed in the order they were encountered</span></b> in.

With [[Year 3/Sem 2/CS4218 - Software Testing/A Guide To Jest.md#Hooks|hooks]] it will call `before*` & `after*` in <b><span style='color: #FFD700'>order of declaration</span></b>. The **only exception** is <b><span style='color: #FFD700'>enclosing</span></b> `after*`, where it is <b><span style='color: #FFD700'>based on the closest</span></b> `after*` hook.

>[!example] Example of order of execution
>```js
>beforeEach(() => console.log('connection setup'));
>beforeEach(() => console.log('database setup'));
>
>afterEach(() => console.log('database teardown'));
>afterEach(() => console.log('connection teardown'));
>
>test('test 1', () => console.log('test 1'));
>
>describe('extra', () => {
 >	beforeEach(() => console.log('extra database setup'));
 >	afterEach(() => console.log('extra database teardown'));
>
>	test('test 2', () => console.log('test 2'));
>});
>```
>The following will be printed out:
>1) connection setup
>2) database setup
>3) test 1
>4) database teardown
>5) connection teardown
>6) connection setup
>7) database setup
>8) extra database setup
>9) test 2
>10) extra database teardown
>11) database teardown
>12) connection teardown
# Mocking
---
In <b><span style='color: #DDA0DD'>Jest</span></b>, the concept of <b><span style='color: #FFD700'>stubbing & mocking is combined</span></b> into 1 module.

To **mock a function** use the `jest.fn(...)`

>[!example] Example of mocking a function
>```js
>jest.fn(x -> x + x);
>```

We can also **mock entire modules** using the `jest.mock(...)`. Then we need to <b><span style='color: #FFD700'>specify what the function should return</span></b> when its called.

>[!example] Example of mocking the `axios` module
>```js
>import axios from 'axios';
>jest.mock('axios');
>// Need to specify what the function needs to do when its called
>axios.post.mockResolvedValueOnce({ data: { success: true } });
>```

>[!important] For mocked modules, the entire implementation will be striped away

Some ways to mock return values:
- `mockResolvedValueOnce`, to specify what to return once (*if the function is called 2 times then you need to specify twice*)
- `mockResolvedValue`, mainly what to return for async functions
- `mockReturnValie`, to define what the function to return, for non async functions
- `mockRejectedValue`, to define an error to throw for the particular function
## Static Vs Non-Static Functions

For **regular functions which are not in a class**, you can mock the return value by doing `fn_name.`.

Now for **classes**, for **non static functions** we need to <b><span style='color: #FFD700'>mock the constructor & all the relevant functions</span></b>. We can do it like so:

```js
categoryModel.mockImplementation(() => ({
	// You return an Object (The Instance) containing... 
	// The Non-Static Function (like .save) 
	save: jest.fn().mockResolvedValue(savedCategory) 
}));
```

For **static functions** we can directly call the function for instance `class.fn_name.`.
## Spying

If the internal implementation is important (*& you do not want strip away the implementation during mocking*) you can <b><span style='color: #FFD700'>spy on the function to verify interactions</span></b>.

use the `jest.spyOn(object, function)` function to spy on a particular function within an object.

>[!example] Example of spying on a function
>```js
>const video = {
>	play () {
>		return true;
>	},
>};
>test ('plays video', () => {
>	const spy = jest.sptOn(video, 'play');
>	const isPlaying = video.play();
>	expect(spy).toHaveBeenCalled();
>});
>```
# Hooks
---
There are useful <b><span style='color: #DDA0DD'>hooks</span></b> to be used which can help set up variables before a test, do a clean up after each test or once all the test have been completed.

>[!important] Functions that are being spied on will persist on to the next test case so we need to explicitly clear it that is one use case of hooks

These are some of the hooks:
- `beforeAll` (*runs before all test cases, to set up variables*)
- `afterAll` (*runs after all test cases, for cleanup if necessary*)
- `beforeEach` (*runs before each test case*)
- `afterEach` (*runs after each test case*)

