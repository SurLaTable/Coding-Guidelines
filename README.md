# Coding Guidelines

![Cali-Mongo](https://scontent-lax3-1.xx.fbcdn.net/t31.0-8/14196062_508726895991144_2686693989240624443_o.png)

* Use American spelling.
* Use tabs to indent. This applies to all MongoDB-specific code (chained functions) and objects used by MongoDB (queries, projections, documents).
* Always have a space after a : colon.
* Comma-last.

If you divide the components of an object/array into various lines, use one line for each component. The } *closing curly brace* should follow the last component (except for aggregation).

**Good**

```javascript
{ 
	$sort: {
		'population': -1, 
		'_id.state': 1,
		‘zipCode’: 1
	} 
}

// Also

var proj = { 
	_id: 0, 
	a: 1, 
	b: 1, 
	c: 1, 
	d: 1, 
	e: 1 };

```
**Bad**
```javascript
{ 
	$sort: {
		'population': -1, '_id.state': 1,
		‘zipCode’: 1
	} 
}

// Or

var proj = { _id: 0, a: 1, b: 1, 
	c: 1, d: 1, e: 1 };

```

* No _ underscores in the middle of names (database, collection, fields) except for manual references.
* Collections database, variables, properties and function names should use lowerCamelCase. They should also be descriptive. Single character variables and uncommon abbreviations should generally be avoided.
* Place spaces between nested parentheticals and elements in JavaScript examples. For example, prefer __{ [ a, a, a ] }__ over __{[a,a,a]}__.

## Collection Names

* Try to have the database named after the project and one database per project.
* Use camelCase.
* A database with “” empty string is not a valid database name.
* Database name cannot be more than 64 bytes.
* Database name are case-sensitive, even on non-case-sensitive file systems. Thus it is good to keep name in lower case.
* A database name cannot contain any of these characters “/, \, ., “, *, <, >, :, |, ?, $,”. It also cannot contain a single space or null character.

```javascript
```

```javascript
```

```javascript
```

```javascript
```

