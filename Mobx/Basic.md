# ❔What is Mobx
---
**MobX** is a popular state management library that can be used with React and TypeScript. One of the great things about MobX is that it allows you to *store state* in a simple data structure and let the library take care of keeping everything up to date. The MobX API has four simple building blocks at its core: **Observable**, **Actions**, **Computed**, and **Reactions**.


# 🔭Observable
---
An Observable is a way to make an object’s properties reactive. When the data changes, the observable object notifies its observers. To define a property as observable, you can use the `@observable` decorator. For example:

```javascript
class TodoStore {
  @observable todos: Todo[]
}
```

Now when a new value is assigned to the `todos` array, notifications will fire and all associated observers will be notified .

# 🎬Actions
---
An Action is a way to change an observable and update the state. To define an action, you can decorate methods inside the store with `@action`. For example:

```javascript
@action toggleTodo = (id: string) => {
  this.todos = this.todos.map(todo => {
    if (todo.id === id) {
      return { ...todo, completed: !todo.completed };
    }
    return todo;
  });
};
```

In this example, the `toggleTodo` action updates the `completed` property of a todo item in the `todos` array.

# 💻Computed
---
A Computed value can be used to derive values from the existing state or other computed values. To define a computed value, you can use the `@computed` decorator. For example:

```javascript
@computed get info() {
  return {
    total: this.todos.length,
    completed: this.todos.filter(todo => todo.completed).length,
    notCompleted: this.todos.filter(todo => !todo.completed).length
  };
}
```

In this example, the `info` computed value derives information about the `todos` array, such as the total number of todos and the number of completed and not completed todos.

Computed values are commonly used to derive new information from the existing state. Some common use cases for computed values include:

-   Deriving information from the state: For example, calculating the total number of completed todos in a todo list.
-   Filtering or sorting data: For example, filtering a list of items based on a search query or sorting a list of items by date.
-   Aggregating data: For example, calculating the sum or average of a set of values.

Computed values are automatically updated whenever the state they depend on changes, making them a powerful tool for keeping your UI in sync with your data.

# 🤔Reactions
---
Reactions are a way to automatically run side effects when an observable changes. Reactions track observables from inside the store itself and can be used to perform actions such as logging, making network requests, or updating other parts of the state.

Here’s an example of using a reaction to log the length of the `todos` array whenever it changes:

```javascript
class TodoStore {
  constructor() {
    reaction(
      () => this.todos,
      _ => console.log(this.todos.length)
    );
  }
}
```

In this example, the reaction takes two arguments: a function that returns the data to track (`() => this.todos`) and a function that runs whenever the tracked data changes (`_ => console.log(this.todos.length)`).