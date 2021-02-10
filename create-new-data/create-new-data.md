## Create a new database
* Just use the 'use' keyword as if it exist 
`use animal_shelter`

`This is the procedure how the database gets called by Mongo 
will automatically save the new database when it has`
* at least one collection
* and that collection at least has one document

### Insert into a collection
``` db.<collection_name>.insert({...})```

```
Inset a new dog named Fluffy into the system:
db.animals.insert({
    'name':'Fluffy',
    'age':3,
    'breed': 'Golden Retriever',
    'species': 'Dog'
})
```


Once we done this step, if the database has not been saved, 
it will be saved 
* mongoDB will then give its own ObjectId()

```
db.animals.insertMany([
    {
        'name':'Muffin',
        'age':3,
        'breed':'Orange Tabby',
        'species':'Cat'
    },
    {
        'name':'Cupcake',
        'age':2,
        'breed':'Whitey Cat',
        'species':'Cat'
    }
])
```
