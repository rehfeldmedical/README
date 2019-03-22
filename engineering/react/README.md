# Introduction

We standardize a number of processes & tooling across our React applications, so that they don't drift too far apart when it comes to cross-cutting concerns. This document summarizes those elements for easy overview.

## TypeScript vs. JavaScript

Our React-based projects are all required to be in TypeScript currently, both for mobile and web.

## Documentation

TODO

## Testing

We use Jest to write tests and Storybook with snapshots as a Proof-of-Concept for components. 

## State management

As a general guideline, our React projects adopt [redux](https://github.com/reduxjs/redux) and [redux-thunk](https://github.com/reduxjs/redux-thunk) to help steer application state and dispatching of asynchronous actions respectively.