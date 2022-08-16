# atlas-search-queries
# using sample data from sample_mflix.movies

## Simple search for godfather
```
[{$search: {
  index: 'default',
  text: {
    query: 'godfather',
    path: 'title'
  }
}}, {$project: {
  _id: 1,
  title: 1,
  genres: 1
}}, {$limit: 5}]
```

## Fuzzy Search
```
[{$search: {
  index: 'fuzzy',
  autocomplete: {
    path: 'title',
    query: 'gadfazher',
    fuzzy: {
      maxEdits: 2,
      prefixLength: 1,
      maxExpansions: 256
    }
  }
}}, {$limit: 10}, {$project: {
  _id: 0,
  title: 1
}}]
```

## More like this
```
[{$search: {
  moreLikeThis: {
    like: {
      title: 'godfather',
      genres: 'action'
    }
  }
}}, {$limit: 5}, {$project: {
  _id: 0,
  title: 1,
  released: 1,
  genres: 1
}}]
```
