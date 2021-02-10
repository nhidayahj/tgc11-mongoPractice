### Hands-On Practice - Create new database

* keep the naming of keys consistent 

1. 
* create a database called - 'fake_school'
* each student braces is called a document,
* added to collection called 'students'
```
use fake_school
```
```
db.students.insertMany([
    {
        'name':'Jane Doe',
        'age':13,
        'subjects':['Defense Against the Dark Arts, Charms History of Magic'],
        'date_enrolled': '13th May 2016'
    },
    {
        'name': 'James Verses',
        'age':14,
        'subjects':['Transfiguration','Alchemy'],
        'date_enrolled': '15th June 2015'
    },
    {
        'name': 'Johnathan Goh',
        'age': 12,
        'subjects':['Divination', 'Study of Ancient Runes'],
        'date_enrolled': '16th April 2017'
    }
])
```

## Update existing document

### Update a documet by its ObjectId

#### 'Prestige method' aka PUT method
* Replaces the entire document, but retain the identity by keeping the old id.
```
db.students.update({
    '_id':ObjectId("602349b28e42018bfd96aceb"),
}, {
    'name':'James Verses',
    'age':15,
    'subjects': [
        'Transfiguration',
        'Alchemy'
    ],
    'date_enrolled': new Date('2015-06-15')
})
```

```
db.students.update({
    '_id':ObjectId("602349b28e42018bfd96acea"),
}, {
    'name':'Jane Doe',
    'age':15,
    'subjects': [
        'Defense Against the Dark Arts',
        'Charms',
        'History of Magic'
    ],
    'date_enrolled': new Date('2016-05-13')
})
```


#### Patch method 
* Updates one or more keys of the existing document
```
db.students.update({
    '_id':ObjectId("602349b28e42018bfd96aceb"),
}, {
    '$set': {
        'age':16
    }
})
```

### Update many 
* updtae all students who's age is >=13 to have fyp 
```
db.students.updateMany({
    'age': {
        '$gt':13
    }
}, {
    '$set': {
        'fyp': true 
    }
})
```

### Delete 
```
db.students.remove({
    '_id': ObjectId("602349b28e42018bfd96aceb")
})
```

```
db.students.remove({
    '_id':ObjectId("602349b28e42018bfd96acec")
})
```

## Manage sub-documents

* Suppose we have a document that looks like this:
```
db.animals.insert({
    'name': 'Cookie',
    'age': 1,
    'breed': 'Beagle',
    'species':'Dog',
    'tags': [
        'playful', 'toilet-trained', 'good with cats'
    ]
})
```

### Push to the back of the tags array for Cookie 
db.animals.update({
    '_id': ObjectId("6023595e8e42018bfd96aced")
}, {
    '$push': {
        'tags':'good with kids'
    }
})

### To remove a certain item from a tag 
* remove 'good with cats' 
```
db.animals.update({
    '_id': ObjectId("6023595e8e42018bfd96aced")
}, {
    '$pull': {
        'tags': 'good with kids'
    }
})
```

### Updating sub-documents
* Imagine we add a sub-document into Cookie
```
db.animals.update({
    '_id': ObjectId("6023595e8e42018bfd96aced")
}, {
    '$set': {
        'vet': {
            'name': 'Dr DoLittle',
            'contact': 999999998,
            'address': 'Sunset Way Blk 3 #01-12'
        }
    }
})
```

* Update DrDolittle to have sirname 'Tan'
```
db.animals.update({
    '_id': ObjectId("6023595e8e42018bfd96aced")
}, {
    '$set': {
        'vet.name': 'Dr Dolittle Tan'
    }
})
```

### Updating a specific Object in an array
* Assume Cookie has a list of checkups he has attended 
```
db.animals.update({
    '_id': ObjectId('6023595e8e42018bfd96aced')
}, {
    '$set': {
        'checkups': [
            {
                '_id': ObjectId(),
                'diagnosis': 'Inflammation',
                'treatment': 'Anti-inflammatory'
            }, 
            {
                '_id': ObjectId(),
                'diagnosis': 'Anxiety',
                'treatment': 'Anxiety Pills'
            },
            {
                '_id': ObjectId(),
                'diagnosis': 'Anger Issue',
                'treatment': 'Constant care'
            }
            
        ]
    }
})
```
* Update checkup of Anxiety diagnosis and change to depression. 

```
db.animals.update({
    'checkups': {
        '$elemMatch': {
            '_id': ObjectId("60235c948e42018bfd96acef")
        }
    }
}, {
    '$set': {
        'checkups.$.diagnosis': "Separation Anxiety",
        'checkups.$.treatment': "Anti-depressant"
    }
})
```