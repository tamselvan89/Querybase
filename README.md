<p align="center">
  <img height="75px" width="411px" src="https://raw.githubusercontent.com/davideast/Querybase/master/logos/logo-large.png">
  <p align="center">Bringing the <code>.where()</code> statement to the Firebase Database</p>
</p>

[![Build Status](https://travis-ci.org/davideast/Querybase.svg?branch=master)](https://travis-ci.org/davideast/Querybase)
[![Coverage Status](https://coveralls.io/repos/github/davideast/Querybase/badge.svg?branch=master)](https://coveralls.io/github/davideast/Querybase?branch=master)

## What is Querybase?

- **.where()** - Find records by multiple fields.
- **No client-side filtering** - Querybase genererates composite keys to provide querying on multiple fields.
- **Simple Query API** - Use common query methods such as `.greaterThan()`, `.lessThan()`, and `.startsWith()`.

## Documentation

Querybase takes a Firebase Database reference with a list of fields to create composite keys. 

### Querying using multiple fields

```js
 const databaseRef = firebase.database().ref().child('people');
 const querybaseRef = querybase.ref(databaseRef, ['name', 'age', 'location']);
 
 // Automatically handles composite keys
 querybaseRef.push({ 
   name: 'David',
   age: 27,
   location: 'SF'
 });
 
// Find records by multiple fields
// returns a Firebase Database ref
const queriedDbRef = querybaseRef
  .where({
    name: 'David',
    age: 27
  });
  
 // Listen for realtime updates
 queriedDbRef.on('value', snap => console.log(snap));
 ```
 
### Querying using one field
 
 ```js
 const databaseRef = firebase.database.ref().child('people');
 const queryRef = querybase.query(databaseRef);
 // Querybase for single criteria, returns a Firebase Ref
 querybaseRef.where({ name: 'David'});
  
 // Querybase for a single string criteria, returns
 // a QuerybaseQuery, which returns a Firebase Ref
 querybaseRef.where('name').startsWith('Da');
 querybaseRef.where('age').lessThan(30);
 querybaseRef.where('age').greaterThan(20);
 querybaseRef.where('age').between(20, 30);
 ```
