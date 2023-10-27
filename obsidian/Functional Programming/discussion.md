# Functional Programming

## 🧦 Paradigms

- How do we abstract? 
- Very simple concept at face value
- Wide range of programming paradigms
- Depends on your definition and scope
- Three that commonly referenced
- Helpful to think as qualities instead

## 🔬 Examples

- Procedural: Impure Functions (side-effects)
- Object-oriented: Objects (co-locate data and behaviour)
- Functional: Pure Functions (composing behaviour)

### Procedural 

```js
peelCarrot() 
cookCarrot()
```

### Object-oriented

```js
const createFood = () => ({
  cooked: false, 
  peeled: false, 
  peel () {
    this.peeled = true;
  }
}) 

const carrot = createFood()
const banana = createFood()

const pot = {
  celsius: 103,
  add: (food) {
    food.cooked = true
  }
}

carrot.peel()
pot.add(carrot)
```

### Functional

```js
const state = {
  carrot: {
    peeled: false, 
    cooked: false, 
   }, 
   banana: {
     peeled: false, 
     cooked: false, 
   }
   pot: {
     celsius: 103,
   }
}

const transform = key => 
  operation => 
    state =>
      ({
       ...state,
       [key]: operation(state[key])
      })

const peel = target => {
  if (target.peel !== false) {
    throw new Error('Not peelable')
  }
  
  return {
    ...target, 
    peeled: true, 
 } 
})

const state = transform('carrot')(peel)(state)
```

## 🚰 Functional Programming

- Immutability: Console log all at end
- Composition/HOF: Functions as values
- Purity: Predictable and testable
- State Discipline: Contain side-effects

## 🌐 Associated Concepts

- Utility Libraries: Lodash, Ramda, RxJS
- Array Methods: Most common HOF
- Unit Tests: Testing input and output 
- Asynchrony: Streaming/piping of data


Tutorial
https://www.youtube.com/watch?v=Z3PLwD3iebg&list=PLuPevXgCPUIMbCxBEnc1dNwboH6e2ImQo