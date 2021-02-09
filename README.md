![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

Welcome nhidayahj,

This is the Code Institute student template for Gitpod. We have preinstalled all of the tools you need to get started. You can safely delete this README.md file, or change it for your own project. Please do read it at least once, though! It contains some important information about Gitpod and the extensions we use.

## Gitpod Reminders

To run a frontend (HTML, CSS, Javascript only) application in Gitpod, in the terminal, type:

`python3 -m http.server`

A blue button should appear to click: *Make Public*,

Another blue button should appear to click: *Open Browser*.

To run a backend Python file, type `python3 app.py`, if your Python file is named `app.py` of course.

A blue button should appear to click: *Make Public*,

Another blue button should appear to click: *Open Browser*.

In Gitpod you have superuser security privileges by default. Therefore you do not need to use the `sudo` (superuser do) command in the bash terminal in any of the lessons.

## Updates Since The Instructional Video

We continually tweak and adjust this template to help give you the best experience. Here is the version history:

**October 21 2020:** Versions of the HTMLHint, Prettier, Bootstrap4 CDN and Auto Close extensions updated. The Python extension needs to stay the same version for now.

**October 08 2020:** Additional large Gitpod files (`core.mongo*` and `core.python*`) are now hidden in the Explorer, and have been added to the `.gitignore` by default.

**September 22 2020:** Gitpod occasionally creates large `core.Microsoft` files. These are now hidden in the Explorer. A `.gitignore` file has been created to make sure these files will not be committed, along with other common files.

**April 16 2020:** The template now automatically installs MySQL instead of relying on the Gitpod MySQL image. The message about a Python linter not being installed has been dealt with, and the set-up files are now hidden in the Gitpod file explorer.

**April 13 2020:** Added the _Prettier_ code beautifier extension instead of the code formatter built-in to Gitpod.

**February 2020:** The initialisation files now _do not_ auto-delete. They will remain in your project. You can safely ignore them. They just make sure that your workspace is configured correctly each time you open it. It will also prevent the Gitpod configuration popup from appearing.

**December 2019:** Added Eventyret's Bootstrap 4 extension. Type `!bscdn` in a HTML file to add the Bootstrap boilerplate. Check out the <a href="https://github.com/Eventyret/vscode-bcdn" target="_blank">README.md file at the official repo</a> for more options.

--------

Happy coding!

# Commands to enter in Terminal

## To show all databases in mongoDB:
```
show databases;
```

## To switch to the specific database:
```
use <name_of_database>;
```

## MUST always show collections after selecting specific database:
```
show collections;
```

## check the currently selected database
```
db
```

## find all documents from a collection:

## To show all documents
```
db.<name_of_collection>.find()
```

## limit the number of documents found
```
db.<name_of_collection>.find().limit(10)
```

## format the output nicely with .pretty()
```
db.<name_of_collection>.find().pretty().limit(10)
db.listingsAndReviews.find().pretty().limit(10)
```
* limit.() must always be LAST

## Projecting 
* show only certains keys from the documents
```
db.listingsAndReviews.find({}, {
    'name':1,
    'summary':1,
    'address':1
}).pretty()
```

### Projecting a sub-document 
```
db.listingsAndReviews.find({}, {
    'name':1,
    'summary':1,
    'address.street':1,
    'address.country':1
}).pretty()
```

### Searching documents by criteria
* find all the listings that has exactly 2 beds
```
db.listingsAndReviews.find({
    'beds':2
}, {
    'name':1,'address':1, 'date':1
}).pretty()
```

* find all the listings with exactly 2 beds and has exactly 2 bedrooms
```
db.listingsAndReviews.find({
    'beds':2,
    'bedrooms':2
}, {
    'name':1, 'address.country':1, 'beds':1, 'bedrooms':1
}).pretty()
```

* Finding by Country
```
db.listingsAndReviews.find({
    'address.country':'Brazil'
}, {
    'name':1, 'address.country':1, 'beds':1, 'bedrooms':1
}).pretty()
```

* Count total number of results with .count()
```
db.listingsAndReviews.find({
    'address.country':'Brazil'
}, {
    'name':1, 'address.country':1, 'beds':1, 'bedrooms':1
}).count()
```

* Find  listings with only 2 beds, 2 bedrooms, and in Brazil -- set the criteria 
```
db.listingsAndReviews.find({
    'address.country':'Brazil',
    'bedrooms':2,
    'beds':2
}, {
    'name':1, 'address.country':1, 'beds':1, 'bedrooms':1
}).pretty()
```

## Find by Inequality using the special character $ 
* Find all listings that have greater than 3 beds 
```
db.listingsAndReviews.find({
    'beds': {
        '$gt':3
    }
}, {
    'name':1, 'beds':1
})
```
* Find all listings that has beds with greater than or equal to 3 
```
db.listingsAndReviews.find({
    'beds': {
        '$gte':3
    }
}, {
    'name':1, 'beds':1
})
```
* Find listings with less than 6 beds
```
db.listingsAndReviews.find({
    'beds': {
        '$lt':6
    }
}, {
    'name':1, 'beds':1
})
```
* Find listings that have between 3 to 6 beds:
```
db.listingsAndReviews.find({
    'beds': {
        '$gte':3,
        '$lte':6
    }
}, {
    'name':1, 'beds':1
})
```

## mongoDB Practice Questions: 
1. 
```
db.companies.find({
    'founded_year':2006
}, {
    'founded_year':1, 'name':1
}).pretty()
```
2. 
```
db.companies.find({
    'founded_year':{
        '$gt':2000
    }
}, {
    'founded_year':1, 'name':1
}).pretty()
```

3.
```
db.companies.find({
    'founded_year': {
        '$gt':1900,
        '$lt':2000
    }
}, {'name':1, 'founded_year':1}).pretty()
```

```
db.companies.find({},
{'name':1, 'ipo':1}).pretty().limit(10)
```

```
db.companies.find({
    'ipo.valuation_amount':{
        '$gt':100000000
    }
}, {
    'name':1, 'ipo.valuation_amount':1, 'ipo.valuation_currency':1
}).pretty()
```

```
db.companies.find({
    'ipo.valuation_amount':{
        '$gt':100000000
    },
    'ipo.valuation_currency_code':'USD'
}, {'name':1, 'ipo.valuation_currency_code':1, 'ipo.valuation_amount':1}).pretty()
```

