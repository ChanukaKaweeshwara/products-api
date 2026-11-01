```mermaid
classDiagram

class Product {
<<abstract>>
- Long id
- String name
- double price
+ getId() Long
+ getName() String
+ getPrice() double
+ getSummary() String*
}

class Discountable {
<<interface>>
+ applyDiscount(rate : double) void
+ getDiscountedPrice() double
}

class DigitalProduct {
- String downloadUrl
- double fileSizeMB
- double discountedPrice
+ getDownloadUrl() String
+ getFileSizeMB() double
+ getSummary() String
+ applyDiscount(rate : double) void
+ getDiscountedPrice() double
}

class PhysicalProduct {
- double weightKg
- String dimensions
- double discountedPrice
+ getWeightKg() double
+ getDimensions() String
+ getSummary() String
+ applyDiscount(rate : double) void
+ getDiscountedPrice() double
}

class ProductService {
- List~Product~ products
- Long nextId
+ getAllProducts() List~Product~
+ addProduct(product : Product) Product
+ getProductById(id : Long) Optional~Product~
+ deleteProduct(id : Long) void
+ findByName(name : String) List~Product~
+ getAllSummaries() List~String~
}

class ProductController {
- ProductService productService
+ getAllProducts() List~Product~
+ getProductById(id : Long) Product
+ addProduct(product : DigitalProduct) Product
+ deleteProduct(id : Long) void
+ search(name : String) List~Product~
+ getSummaries() List~String~
}

Product <|-- DigitalProduct
Product <|-- PhysicalProduct

Discountable <|.. DigitalProduct
Discountable <|.. PhysicalProduct

ProductService --> Product : manages
ProductController ..> ProductService : uses