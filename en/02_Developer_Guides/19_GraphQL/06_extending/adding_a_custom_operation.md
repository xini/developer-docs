---
title: Adding a custom operation
summary: Add a new operation for model types 
---
# Extending the schema

[CHILDREN asList]

## Adding a custom operation

By default, we get basic operations for our models, like `read`, `create`,
`update`, and `delete`, but we can add to this list by creating
an implementation of [`OperationProvider`](api:SilverStripe\GraphQL\Schema\Interfaces\OperationProvider) and registering it.

Let's build a new operation that **duplicates** DataObjects.

```php
class DuplicateCreator implements OperationCreator
{
    public function createOperation(
        SchemaModelInterface $model,
        string $typeName,
        array $config = []
    ): ?ModelOperation
    {
        $mutationName = 'duplicate' . ucfirst(Schema::pluralise($typeName));

        return ModelMutation::create($model, $mutationName)
            ->setType($typeName)
            ->addArg('id', 'ID!')
            ->setDefaultResolver([static::class, 'resolve'])
            ->setResolverContext([
                'dataClass' => $model->getSourceClass(),
            ]);
    }
}
```

We add **resolver context** to the mutation because we need to know
what class to duplicate, but we need to make sure we still have a
static function.

The signature for resolvers with context is:

```php
public static function (array $context): Closure
```

We use the context to pass to a function that we'll create dynamically.
Let's add that now.

```php
public static function resolve(array $resolverContext = []): Closure
{
    $dataClass = $resolverContext['dataClass'] ?? null;
    return function ($obj, array $args) use ($dataClass) {
        if (!$dataClass) {
            return null;
        }
        return DataObject::get_by_id($dataClass, $args['id'])
            ->duplicate();
    };
}
```

Now, just add the operation to the `DataObjectModel` configuration
to make it available to all `DataObject` types.

**app/_graphql/config.yml**
```yaml
modelConfig:
  DataObject:
    operations:
      duplicate:
        class: 'MyProject\Operations\DuplicateCreator'
```

And use it:

**app/_graphql/models.yml**
```yaml
MyProject\Models\MyDataObject:
  fields: '*'
  operations:
    read: true
    duplicate: true
```

### Further reading

[CHILDREN]
