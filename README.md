# Forklift

Forklift a Generic Repository Pattern engine, made to support multiple abstraction of Domain-Driven Design repository implementations.

ORM/ActiveRecords implementations
- PHP InMemory - In progress
- Laravel Eloquent - In progress
- Doctrine ORM - In progress
- Redis - In progress
- REST (Guzzle) - In progress

## Save Implemention Propose(Beta)
```php
<?php

use Peroxide\Forklift\GenericRepository;
use Peroxide\Forklift\Adapter\InMemoryAgent;

$repository = new GenericRepository(new InMemoryAgent());
$repository->setCollection('products');

$entity = new Product();

// Persisting an Entity in products collection
$repository->save($entity);
$repository->flush();
```

## Filter Implemention Propose(Beta)
```php
<?php

use Peroxide\Forklift\GenericRepository;
use Peroxide\Forklift\Adapter\InMemoryAgent;

$repository = new GenericRepository(new InMemoryAgent());

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
