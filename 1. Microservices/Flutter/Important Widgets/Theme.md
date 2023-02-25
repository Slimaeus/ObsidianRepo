## 1. Docs
[Docs](https://docs.flutter.dev/cookbook/design/themes)

## 2. Usage
```dart
var themeData = ThemeData(
	primarySwatch: Colors.purple,
	colorScheme: ThemeData.light()
		.colorScheme
		.copyWith(secondary: Colors.deepOrange),
	fontFamily: 'Lato');

var primaryCol = Theme.of(context).primaryColor;
```