---
title: Property mapping and dot syntax
summary: Learn how to customise field names, use dot syntax, and use aggregate functions
---

# Working with DataObjects

[CHILDREN asList]

## Property mapping and dot syntax

For the most part, field names are inferred through the `DataObject` model, but its API affords developers full
control over naming.

In this example, we are taking a property `content` (which will be defined as `Content` in php) and defining it
as `pageContent` for GraphQL queries and mutations.

**app/_graphql/models.yml**
```yaml
Page:
  fields:
    pageContent:
      type: String
      property: Content
```

[notice]
When using explicit property mapping, you must also define an explicit type, as it can
no longer be inferred.
[/notice]

### Dot-separated accessors

Property mapping is particularly useful when using **dot syntax** to access fields.

**app/_graphql/models.yml**
```yaml
MyProject\Pages\Blog:
  fields:
    title: true
    authorName:
      type: String
      property: 'Author.FirstName'
```

Fields on `has_many` or `many_many` relationships will automatically convert to a `column` array:

**app/_graphql/models.yml**
```yaml
MyProject\Pages\Blog:
  fields:
    title: true
    categoryTitles:
      type: '[String]'
      property: 'Categories.Title'
    authorsFavourites:
      type: '[String]'
      property: 'Author.FavouritePosts.Title'
```

We can even use a small subset of **aggregates**, including `Count()`, `Max()`, `Min()` and `Avg()`.

**app/_graphql/models.yml**
```yaml
MyProject\Models\ProductCategory:
  fields:
    title: true
    productCount:
      type: Int
      property: 'Products.Count()'
    averageProductPrice:
      type: Float
      property: 'Products.Avg(Price)'
```

### Further reading

[CHILDREN]
