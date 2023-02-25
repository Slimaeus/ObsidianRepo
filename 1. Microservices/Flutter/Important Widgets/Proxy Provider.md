## 1. Docs
[Docs](https://pub.dev/documentation/provider/latest/provider/ChangeNotifierProxyProvider-class.html)

## 2. Usage
Example 
```dart
ChangeNotifierProxyProvider<Auth, Products>(
	create: (ctx) => null,
	update: (ctx, auth, previousProducts) => Products(auth.token,
		previousProducts == null ? [] : previousProducts.items)),
```