# bind-decorator

Context method binding decorator.

[![npm version](https://badge.fury.io/js/react-component-ref.svg)](https://badge.fury.io/js/react-component-ref)
[![license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/NoHomey/react-component-ref)
[![Build Status](https://semaphoreci.com/api/v1/nohomey/react-component-ref/branches/master/badge.svg)](https://semaphoreci.com/nohomey/react-component-ref)

`@bind` is just a little faster version of [`@autobind`](https://github.com/andreypopp/autobind-decorator/blob/master/src/index.js) for decorating methods only, by binding them to the current context. It is written in TypeScript and follows the latest `decorator`s [purposal](http://tc39.github.io/proposal-decorators/).

- It will `throw` exceptions if decorating anything other than `function`;
- Since the implementation follows the latest `decorator`s [purposal](http://tc39.github.io/proposal-decorators/) where compartion betweeen `this` and `target` can not be trusted, `@bind` will always `return` a `configurable`, `get accessor propertyDescriptor` which will memomize the result of `descriptor.value.bind(this)` by re-defining the property descriptor of the method beeing decorated (Credits goes to [autobind-decorator](https://github.com/andreypopp/autobind-decorator/blob/master/src/index.js) for memoizing the result).

If you are looking for not just method decorator but rather full class bounding decorator check [`@autobind`](https://github.com/andreypopp/autobind-decorator/blob/master/src/index.js).

# Install

[![NPM](https://nodei.co/npm/bind-decorator.png?downloads=true&stars=true)](https://nodei.co/npm/bind-decorator/)

# Usage

## In JavaScript

```javascript
import bind from 'bind-decorator';

class Test {
    static what = 'static';
    
    @bind
    static test() {
        console.log(this.what);
    }

    constructor(what) {
        this.what = what;
    }

    @bind
    test() {
        console.warn(this.what);
    }
}

const tester = new Test('bind');
const { test } = tester;
tester.test(); // warns 'bind'.
test(); // warns 'bind'.
Test.test(); // logs 'static'.
```

## In TypeScript

```typescript
import bind from 'bind-decorator';

class Test {
    public static what: string = 'static';
    
    @bind
    public static test(): void {
        console.log(this.what);
    }

    public constructor(public what: string) {
        this.what = what;
    }

    @bind
    public test(): void {
        console.warn(this.what);
    }
}

const tester: Test = new Test('bind');
const { test } = tester;
tester.test(); // warns 'bind'.
test(); // warns 'bind'.
Test.test(); // logs 'static'.
```

