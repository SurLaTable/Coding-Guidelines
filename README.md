# Coding Guidelines

![Cali-Mongo](https://scontent-lax3-1.xx.fbcdn.net/t31.0-8/14196062_508726895991144_2686693989240624443_o.png)

## Table of Contents

* [General Guidelines](#general-guidelines)
* [Collection Names](#collection-names)
* [Database Names](#database-names)
* [Field Names](#field-names)
* [Functions](#functions)
* [Aggregation](#aggregation)
* [File Naming Convention](#file-naming-convention)

## <a name="general-guidelines">General Names

* Use American spelling.
* Use tabs to indent. This applies to all MongoDB-specific code (chained functions) and objects used by MongoDB (queries, projections, documents).
* Always have a space after a : _colon_.
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

* No _ _underscores_ in the middle of names (database, collection, fields) except for manual references.
* Collections database, variables, properties and function names should use lowerCamelCase. They should also be descriptive. Single character variables and uncommon abbreviations should generally be avoided.
* Place spaces between nested parentheticals and elements in JavaScript examples. For example, prefer __{ [ a, a, a ] }__ over __{[a,a,a]}__.

## <a name="collection-names">Collection Names

* Try to have the database named after the project and one database per project.
* Use camelCase.
* A database with “” *empty string* is not a valid database name.
* Database name cannot be more than 64 bytes.
* Database name are case-sensitive, even on non-case-sensitive file systems. Thus it is good to keep name in lower case.
* A database name cannot contain any of these characters “/, \, ., “, *, <, >, :, |, ?, $,”. It also cannot contain a single space or null character.

## <a name="database-names">Database Names

* Use camelCase.
* A database with “” *empty string* is not a valid database name.
* Database name cannot be more than 64 bytes.
* Database name are case-sensitive, even on non-case-sensitive file systems. Thus it is good to keep name in lower case.
* A database name cannot contain any of these characters *“/, \, ., “, *, <, >, :, |, ?, $,”*. It also cannot contain a single space or null character.

## <a name="field-names">Field Names

* Use camelCase.
* Don’t use _ *underscore* as the starting character of the field name. The only field with _ undescore should be _id.
* Field names cannot contain . dots or null characters and must not start with a $ *dollar sign*.

Manual references are named after the referenced collection. Use the document type (collection name in singular) followed by _id ( <document>_id ). This is the only case where you can use underscore in the middle.

For example, in a dogs collection, a document would have manual references to external documents named like this:

```javascript
{
	name: 'fido',
	owner_id: '5358e4249611f4a65e3068ab',
	race_id: '5358ee549611f4a65e3068ac',
	colour: 'yellow'
	...
}
```

## <a name="functions">Functions

* One method per line should be used when chaining methods.
* You should also indent these methods with a tab so it's easier to tell they are part of the same chain.

If you need to use a long query, projection or options object for a function, assign it to a var and use the var in the function call to improve readability.

**Good**

```javascript
var proj = { 
	_id: 0, 
	a: 1, 
	b: 1, 
	c: 1, 
	d: 1, 
	e: 1 };

db.zips.find( { a: 2 },  proj );
```

**Bad**

```javascript
db.zips.find( { a: 2 }
, { _id: 0
	, a: 1
	, b: 1
	, c: 1
	, d: 1
	, e: 1} );
```
## <a name="aggregation">Aggregation

* Use one tab as indentation for each level.
* Comma first.

The { } *curly braces* enclosing a whole stage (including its name) will be on the same level as the aggregate function.

**Example:**
```javascript
db.zips.aggregate( [
{
	$match: 
		{ $or: [ {state:'CA'}, {state:'NY'} ] }
}
```

Unary operators ($gt, $lte, $sum, $avg, etc), their operands, and the field they affect go on a single line.

**Good**

```javascript
{
	$match: 
		{ $or: [ {state:'CA'}, {state:'NY'} ] }
}
```
**Bad**

```javascript
{
	$match: 
		{ $or: [ 
			{state:'CA'}, 
			{state:'NY'} 
		]
	}
}
```

If there is only one component/object in the stage or if it’s a logical operator (*and, or*), the { *opening braces* and } *closing braces* after the stage name should go on that same line.

**Good**

```javascript
{
	$match: 
		{ $or: [ { state:'CA' }, { state:'NY' } ] }
},
{ 
	$sort: 
		{ 'population': -1 } 
}
```

**Bad**

```javascript
{
	$match: 
		{ $or: [ 
			{ state:'CA' },
 			{ state:'NY' } ] 
		}
},
{
	$sort: { 'population': -1 } 
}
```

Otherwise, the name of the stage and the { *opening curly brace* of its block should be on the same line, and the } *closing bracket* of the stage will be on its own line.

**Good**

```javascript
{ 
	$group: {
		_id: {
			city: '$city',
			state: '$state' },
		population: { $sum: '$pop' } 
	}
}
```

**Bad**

```javascript
{	
	$group: 
	{
		_id: {
			city: '$city',
			state: '$state' },
		population: { $sum: '$pop' }  }
}
```

Use a new line for each component.

**Example**
```javascript
{ 
	$sort: {
		'population': -1, 
		'_id.state': 1 
	} 
}
```

The ] *closing bracket* of the aggregation stages array will not share the line with the } *closing curly brace* of a stage.

**Good**

```javascript
db.zips.aggregate( [
{
	$match:
		{ $or: [ {state:'CA'}, {state:'NY'} ] }
}
] );
```

**Bad**

```javascript
db.zips.aggregate( [
{
	$match:
		{ $or: [ {state:'CA'}, {state:'NY'} ] }
} ] );
```

Example of aggregation with the above rules:

```javascript
db.zips.aggregate( [
{
	$match: 
		{ $or: [ {state:'CA'}, {state:'NY'} ] }
},
{ 
	$group: {
		_id: {
			city: '$city',
			state: '$state' },
		population: { $sum: '$pop' } 
	}
},
{
	$match: 
		{ 'population': { $gt: 25000 } } 
},
{ 
	$sort: {
		'population': -1, 
		'_id.state': 1 
	} 
},
{
	$group: { 
		_id: null,
		avg: { $avg: '$population' } 
	}
}
] );
```

## <a name="file-naming-convention">File Naming Convention

* Separate words with hyphens (i.e. -.)
* File names should have a terse one or two word name that describes the material covered in the document. Allow the path of the file within the document tree to add some of the required context/categorization. For example it’s acceptable to have /core/sharding.rst and /administration/sharding.rst.

**Source**

* [https://docs.mongodb.com/manual/meta/style-guide](https://docs.mongodb.com/manual/meta/style-guide)
* [https://docs.mongodb.com/manual/faq/fundamentals/#faq-small-documents](https://docs.mongodb.com/manual/faq/fundamentals/#faq-small-documents)
* [https://github.com/mongodb/mongo/wiki/Server-Code-Style](https://github.com/mongodb/mongo/wiki/Server-Code-Style)
* [http://www.learnit.net.in/2016/03/schema-design-and-naming-conventions-in.html](http://www.learnit.net.in/2016/03/schema-design-and-naming-conventions-in.html)
* [https://github.com/felixge/node-style-guide](https://github.com/felixge/node-style-guide)