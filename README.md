# Peroxide - Forklift

Forklift a Generic Repository Pattern engine, made to support multiple abstraction of Domain-Driven Design repository implementations.

ORM/ActiveRecords implementations
- PHP InMemory - Starting papers
- Laravel Eloquent - In progress
- Doctrine ORM - In progress
- MongoDB - In progress
- Redis - In progress
- REST (Guzzle) - In progress

## Save Implemention Propose(Beta)
```php
<?php

use Peroxide\Forklift\GenericRepository;
use Peroxide\Forklift\Adapter\InMemoryStrategy;

$repository = new GenericRepository(new InMemoryStrategy());
$repository->setCollection('products');

$entity = new Product();

// Persisting an Entity in products collection in memory
// ex: array{'products': [ Product{...} ]}
$repository->save($entity);
$repository->flush();
```

## Filter Implemention Propose(Beta)
```php
<?php

use Peroxide\Forklift\GenericRepository;
use Peroxide\Forklift\Adapter\InMemoryStrategy;

$repository = new GenericRepository(
  new InMemoryStrategy(require __DIR__ . '/dump_db_array.php')
);

// Produce a Query like:
// name = 'My product' AND active is true
// ORDER BY name DESC
$criteria = (new CriteriaBuilder())
                  ->equal('name', 'My product')
                  ->equal('active', true)
                  ->orderBy('name', 'DESC')
;

$repository->setMapperObject(Product::class);

// Array of object Product
$products = $repository->collection('products')
                       ->matching($criteria);
```
## Patterns Included
1. Generic Repository
2. Specification
3. Filter/Criteria
4. Data Mapping
5. Unity Of Work
6. State
7. Flyweight
8. Iterator
9. Strategy
10. Chain of Responsibility
