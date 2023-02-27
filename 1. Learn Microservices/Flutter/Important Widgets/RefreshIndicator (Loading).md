#Loading 
## 1. Docs
## 2. Usage
Example: 
```dart
RefreshIndicator(
	onRefresh: () => _refreshProducts(context),
	child: Padding(
	  padding: EdgeInsets.all(8),
	  child: ListView.builder(
		itemBuilder: (_, i) => Column(
		  children: [
			UserProductItem(
				productsData.items[i].id,
				productsData.items[i].title,
				productsData.items[i].imageUrl),
			Divider(),
		  ],
		),
		itemCount: productsData.items.length,
	  ),
	),
  )
```