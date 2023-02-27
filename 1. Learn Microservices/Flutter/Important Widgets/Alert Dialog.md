## 1. Docs
## 2. Usage
```dart
var dialog = AlertDialog(
  title: Text('Are you sure?'),
  content: Text('Do you want to remove the item in the cart?'),
  actions: [
	TextButton(
		onPressed: () {
		  Navigator.of(ctx).pop(false);
		},
		child: Text('No')),
	TextButton(
		onPressed: () {
		  Navigator.of(ctx).pop(true);
		},
		child: Text('Yes'));
```