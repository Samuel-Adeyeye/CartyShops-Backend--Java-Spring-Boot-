# CartyShops

## Overview
A RESTful API backend for an e-commerce shopping cart system built with Java Spring Boot. This project demonstrates implementation of complex entity relationships, RESTful endpoints, and database management using Spring Data JPA.

## Tech Stack
- **Language:** Java 17
- **Framework:** Spring Boot 3.x
- **Database:** MySQL
- **Build Tool:** Maven

## Key Features
- Product management with categories
- Multi-image support for products
- Category-based product organization
- RESTful API endpoints
- Database relationship management
- Error handling and validation

## Entity Relationships
### Product Entity
```java
@Entity
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String brand;
    private BigDecimal price;
    private int inventory;
    private String description;

    @ManyToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "category_id")
    private Category category;

    @OneToMany(mappedBy = "product", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Image> images;
}
```

### Category Entity
```java
@Entity
public class Category {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;


    @OneToMany(mappedBy = "category")
    private List<Product> products;
}
```

### Image Entity
```java
@Entity
public class Image {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String fileName;
    private String fileType;

    @Lob
    private Blob image;
    private String downloadUrl;

    @ManyToOne
    @JoinColumn(name = "product_id")
    private Product product;
}

```

## API Endpoints

### Products
- `GET /api/v1/products` - Get all products
- `GET /api/v1/products/{id}` - Get product by ID
- `POST /api/v1/products` - Create new product
- `PUT /api/v1/products/{id}` - Update product
- `DELETE /api/v1/products/{id}` - Delete product

### Categories
- `GET /api/v1/categories` - Get all categories
- `GET /api/v1/categories/{id}` - Get category by ID
- `POST /api/v1/categories` - Create new category
- `PUT /api/v1/categories/{id}` - Update category
- `DELETE /api/v1/categories/{id}` - Delete category

### Product Images
- `POST /api/v1/products/{id}/images` - Add image to product
- `DELETE /api/v1/products/{id}/images/{imageId}` - Remove image from product

## Setup and Installation

1. Clone the repository:
```bash
git clone https://github.com/Samuel-Adeyeye/CartyShops-Backend--Java-Spring-Boot-.git
```

2. Configure database in `application.properties`:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/carty_shops_db

spring.datasource.username=your_username
spring.datasource.password=your_password
```

3. Run the application:
```bash
mvn spring-boot:run
```

## Database Configuration
The application uses MySQL as the primary database. Configure your database connection in `application.properties`:

```properties
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
```

## Testing
Run tests using Maven:
```bash
mvn test
```

## Project Structure
```
src
├── main
│   ├── java
│   │   └── com.samueladeyeye.cartyshops
│   │       └── project
│   │           └── cartyshops
│   │               ├── controller
│   │               ├── model
│   │               ├── repository
│   │               ├── service
│   │               └── exception
│   └── resources
│       └── application.properties
└── test
    └── target
        └── classes
        └── generated-sources
                
```

## Contributing
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/NewFeature`)
3. Commit your changes (`git commit -m 'Add some NewFeature'`)
4. Push to the branch (`git push origin feature/NewFeature`)
5. Open a Pull Request

## Future Enhancements
- User authentication and authorization
- Shopping cart functionality
- Order processing
- Payment integration
- Product reviews and ratings
- Inventory management

## License
This project is licensed under the MIT License

## Contact
- Project Link: [CartyShops](https://github.com/Samuel-Adeyeye/CartyShops-Backend--Java-Spring-Boot)

- Connect: 
[Email](samueladeyeye2012@gmail.com) |
[LinkedIn](https://www.linkedin.com/in/samuel-adeyeye/)