## 1. Docs
## 2. Usage 
Example
```dart
FutureBuilder(
        future: _refreshProducts(context),
        builder: (ctx, snapshot) =>
            snapshot.connectionState == ConnectionState.waiting
                ? Center(
                    child: CircularProgressIndicator(),
                  )
                : RefreshIndicator(
                    onRefresh: () => _refreshProducts(context),
                    child: Consumer<Products>(
                      builder: (ctx, productsData, child) => Padding(
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
                    ),
                  ),
      )
```