## 1. Docs
[Docs](https://docs.flutter.dev/cookbook/design/snackbars)
## 2. Usage
```dart
const snackBar = SnackBar(
  content: Text('Yay! A SnackBar!'),
);

// Find the ScaffoldMessenger in the widget tree
// and use it to show a SnackBar.
ScaffoldMessenger.of(context).showSnackBar(snackBar);
```
