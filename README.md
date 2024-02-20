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
$repository->setCollection('products');

// Produce a Query like:
// name = 'My product' and active => true
// 
$criteria = new Criteria();
$criteria->equal('name', 'My product')
         ->equal('active', true)
         ->orderBy('name', 'DESC')
;

// Array of products
$products = $repository->matching($criteria);
```
