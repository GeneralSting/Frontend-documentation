# Generators

## Generator basics

### Generator functions

- generators can be paused mid-execution
- execution can be resumed from the point they were paused
- regular functions: run-to-completion, once triggered, they run until done

- generator is also an iterator
  - use it with for...of loop
  - combine it with the spread operator

#### Generators and yield

- generators don't run it he usual way
- special object to run it step-by-step
- pause is indicated by the yield keyword
- yield can be used comparable to the return keyword

#### Use cases for generators

- retrieving a series of values
- generators are optimized for memory
- can be used for streaming data
- generating values
- lazy evaluation
- asynchronous programming

#### Executing a generator function

- in order to execute we need to have:
  - generator
  - generator object
  - execute the generator

```js
function* inventoryGenerator() {
  yield "Smartphone";
  yield "Laptop";
  yield "Tablet";
}

const inventory = inventoryGenerator();
console.log(inventory.next().value); // Smartphone

for (const item of invetoryGenerator()) {
  console.log(item); // Smartphone Laptop Tablet
}

const allItems = [...inventoryGenerator()];
console.log(allItems); // ['Smartphone', 'Laptop', 'Tablet']
```

- two way street: data can be sent back to the generator

```js
function* feedbackGenerator() {
  const firstFeedback = yield "How was your experience?";
  console.log(`feedback received: ${firstFeedback}`);

  const secondFeedback = yield "Any improvement suggestions?";
  console.log(`Feedback received: ${secondFeedback}`);
}

const feedback = feedbackGenerator();

console.log(feedback.next().value); // How was your experience?
console.log(feedback.next("Great").value); // Feedback received: Great
// Any improvement suggestions?
console.log(feedback.next("More tutorials").value); //Feedback received: More tutorials
// undefined -> no values yielded at end
```

- processing the result of next()

```js
function* inventoryGenerator() {
  yield "Smartphone";
  yield "Laptop";
  yield "Tablet";
}

console.log(inventory.next()); // {value: 'Smartphone', done: false}
console.log(inventory.next()); // {value: 'Laptop', done: false}
console.log(inventory.next()); // {value: 'tablet', done: false}
console.log(inventory.next()); // {value: 'undefined', done: true}
```

- delegating generators with yield

```js
function* regularOrderGenerator() {
  yield "Order #1001";
  yield "Order #1002";
}

function* expressOrderGenerator() {
  yield "Order #1003";
  yield "Order #1004";
}

function* orderProcessingGenerator() {
  yield regularOrderGenerator();
  yield expressOrderGenerator();
}

const orderProcessing = orderProcessingGenerator();

consolg.log(orderProcessing.next().value); // Order #1001
```

#### Use cases for canceling execution

- resource management
- long-running tasks
- user interactions
- error handling
- async flow control

---

### Generator patterns

#### IIFE - Immediately Invoked Function Expression

- async/await with generators

```js
async function* productStream() {
  let nextPageUrl = "/api/products?page=1";
  while (nextPageUrl) {
    const response = await fetch(nextPageUrl);
    const data = await response.json();
    nextPageUrl = data.nextPageUrl;
    for (const product of data.products) {
      yield product;
    }
  }
}

(async () => {
  for await (const product of productStream()) {
    displayProduct(produc);
  }
})();
```

#### Handling erros in generators

- try/catch inside generator does not causes crash
- yields an error message
- error message can be logged or handled

```js
function* errorGenerator() {
  try {
    yield "Start yield";
    throw new Error("generator error");
  } catch (error) {
    yield `ERROR: ${error.message}`;
  }
  yield "End yield";
}

for (let item of errorGenerator()) {
  console.log("item: " + item); // item: Start yield
  // item: ERROR: generator error
  // item: End yield
}
```

#### Combining promises and generators

- managing asynchronous code in a synchronous way
- generators can yield promises
- allows a function to pause until the promise is resolved
- can be combined with the use of an external iterator to resume execution
- the value of the promise can then be given back to the generator

```js
function* orderProcessingGenerator(orderId) {
  yield checkInventory(orderId);
  yield processPayment(orderId);
  yield updateOrderStatus(orderId, completed);
}

funciton handleGenerator(gen) {
  const iterator = gen();
  function step(value) {
    const result = iterator.next(value)
    if(!result.done) {
      result.value.then(step).catch(err => console.log(err))
    }
  }
  step();
}

// sample async functions
function checkInventory(orderId) {
  console.log(`Checking inventory for order ${orderId}`)
  return Promise.resolve();
}

function processPayment(orderId) {
  console.log(`Processing payment for order ${orderId}`)
  return Promise.resolve();
}

function updateOrderStatus(orderId, status) {
  console.log(`Updating order ${orderId} to status ${status}`)
  return Promise.resolve();
}

handleGenerator(() => prderProcessingGenerator(123))
```
