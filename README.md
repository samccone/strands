### Strands

A Router based around state and Promise based resolvers.

Each route is defined under a "state key" that is decoupled from the route.
Every state can define `before` and `after` tasks.

`before` tasks are evaluated before the previous state is left, the route will not change until all have been resolved. (if any throw or are rejected the state will not change)
`after` tasks are evaluated after the state has changed.

```js
myRouter = new Strands({
  "edit-cat": {
    route: "cat/edit/:id",
    before: [fetchCat],
    after:  [saveSave]
  }
})

myRouter.go("edit-cat");

function fetchCat(params) {
  return fetch("cat");
}

function saveCat() {
  return fetch("cat", {
    method: "post",
    body: serializeCat()
  })
}
```
