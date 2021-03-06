# GraphQL.js

The JavaScript reference implementation for GraphQL, a query language for APIs created by Facebook.

[![npm version](https://badge.fury.io/js/graphql.svg)](http://badge.fury.io/js/graphql)
[![Build Status](https://travis-ci.org/graphql/graphql-js.svg?branch=master)](https://travis-ci.org/graphql/graphql-js?branch=master)
[![Coverage Status](https://coveralls.io/repos/graphql/graphql-js/badge.svg?branch=master)](https://coveralls.io/r/graphql/graphql-js?branch=master)

See more complete documentation at http://graphql.org/ and
http://graphql.org/graphql-js/.

For questions, ask [Stack Overflow](http://stackoverflow.com/questions/tagged/graphql).

For discussion, join [#graphql on Discord](http://join.reactiflux.com/).


## Getting Started

An overview of GraphQL in general is available in the
[README](https://github.com/facebook/graphql/blob/master/README.md) for the
[Specification for GraphQL](https://github.com/facebook/graphql). That overview
describes a simple set of GraphQL examples that exist as [tests](src/__tests__)
in this repository. A good way to get started with this repository is to walk
through that README and the corresponding tests in parallel.

### Using GraphQL.js

Install GraphQL.js from npm

```sh
npm install --save graphql
```

GraphQL.js provides two important capabilities: building a type schema, and
serving queries against that type schema.

First, build a GraphQL type schema which maps to your code base.

```js
import {
  graphql,
  GraphQLSchema,
  GraphQLObjectType,
  GraphQLString
} from 'graphql';

var schema = new GraphQLSchema({
  query: new GraphQLObjectType({
    name: 'RootQueryType',
    fields: {
      hello: {
        type: GraphQLString,
        resolve() {
          return 'world';
        }
      }
    }
  })
});
```

This defines a simple schema with one type and one field, that resolves
to a fixed value. The `resolve` function can return a value, a promise,
or an array of promises. A more complex example is included in the top
level [tests](src/__tests__) directory.

Then, serve the result of a query against that type schema.

```js
var query = '{ hello }';

graphql(schema, query).then(result => {

  // Prints
  // {
  //   data: { hello: "world" }
  // }
  console.log(result);

});
```

This runs a query fetching the one field defined. The `graphql` function will
first ensure the query is syntactically and semantically valid before executing
it, reporting errors otherwise.

```js
var query = '{ boyhowdy }';

graphql(schema, query).then(result => {

  // Prints
  // {
  //   errors: [
  //     { message: 'Cannot query field boyhowdy on RootQueryType',
  //       locations: [ { line: 1, column: 3 } ] }
  //   ]
  // }
  console.log(result);

});
```

### Want to ride the bleeding edge?

The `npm` branch in this repository is automatically maintained to be the last
commit to `master` to pass all tests, in the same form found on npm. It is
recommend to use builds deployed npm for many reasons, but if you want to use
the latest not-yet-released version of graphql-js, you can do so by depending
directly on this branch:

```
npm install graphql@git://github.com/graphql/graphql-js.git#npm
```

### Contributing

We actively welcome pull requests, learn how to
[contribute](https://github.com/graphql/graphql-js/blob/master/CONTRIBUTING.md).

### Changelog

Changes are tracked as [Github releases](https://github.com/graphql/graphql-js/releases).

### License

GraphQL is [BSD-licensed](https://github.com/graphql/graphql-js/blob/master/LICENSE).
We also provide an additional [patent grant](https://github.com/graphql/graphql-js/blob/master/PATENTS).
