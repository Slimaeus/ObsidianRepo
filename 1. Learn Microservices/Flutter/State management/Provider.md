## 1. Pub.dev
[Install](https://pub.dev/packages/provider/install)
In pubspec.yaml
```yaml
dependencies:
  provider: ^6.0.5
```
## 2. Usage
- Step 1: Add ChangeNotifier to the class.
- Step 2: Provide data with ChangeNotifierProvider class.
- Step 3: Get the provided instance with Provider.of\<className\>(context) or Consumer\<classname\>.

Example:
In product.dart file:
```dart
import 'package:flutter/foundation.dart';


class Product with ChangeNotifier {

  final String id;

  final String title;

  final String description;

  final double price;

  final String imageUrl;

  bool isFavorite;

  

  Product(

      {@required this.id,

      @required this.title,

      @required this.description,

      @required this.price,

      @required this.imageUrl,

      this.isFavorite = false});

  

  void toggleFavoriteStatus() {

    isFavorite = !isFavorite;

    notifyListeners();

  }

}
```

In product_grid.dart:
```dart
import 'package:flutter/material.dart';

import 'package:flutter_shop_app/providers/products.dart';

import 'package:provider/provider.dart';

import 'package:flutter_shop_app/widgets/product_item.dart';

  

class ProductsGrid extends StatelessWidget {

  @override

  Widget build(BuildContext context) {

    final productsData = Provider.of<Products>(context);

    final products = productsData.items;

    return GridView.builder(

        padding: const EdgeInsets.all(10),

        itemCount: products.length,

        gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(

            crossAxisCount: 2,

            childAspectRatio: 3 / 2,

            crossAxisSpacing: 10,

            mainAxisSpacing: 10),

        itemBuilder: (ctx, i) => ChangeNotifierProvider.value(

              value: products[i],

              child: ProductItem(),

            ));

  }

}
```

In product_item.dart:
```dart
import 'package:flutter/material.dart';

import 'package:flutter_shop_app/providers/product.dart';

import 'package:flutter_shop_app/screens/product_detail_screen.dart';

import 'package:provider/provider.dart';

  

class ProductItem extends StatelessWidget {
  @override

  Widget build(BuildContext context) {

    final product = Provider.of<Product>(context, listen: false);

    return ClipRRect(

      borderRadius: BorderRadius.circular(10),

      child: GridTile(

        child: GestureDetector(

          onTap: () {

            Navigator.of(context).pushNamed(ProductDetailScreen.routeName,

                arguments: product.id);

          },

          child: Image.network(

            product.imageUrl,

            fit: BoxFit.cover,

          ),

        ),

        footer: GridTileBar(

          backgroundColor: Colors.black87,

          leading: Consumer<Product>(

            builder: (ctx, product, _) => IconButton(

              icon: Icon(

                  product.isFavorite ? Icons.favorite : Icons.favorite_border),

              onPressed: () {

                product.toggleFavoriteStatus();

              },

              color: Theme.of(context).colorScheme.secondary,

            ),

          ),

          title: Text(

            product.title,

            textAlign: TextAlign.center,

          ),

          trailing: IconButton(

            icon: Icon(Icons.shopping_cart),

            onPressed: () {},

            color: Theme.of(context).colorScheme.secondary,

          ),

        ),

      ),

    );

  }

}
```