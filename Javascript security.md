<div>

## Understanding Javascript security

<hr style="border:3px solid grey">
<div>

### how browsers execute javascript code:   
- code is downloaded
	- each site gets a sandbox
- multiple security measures
	- OS process separation
	- HTTPS
	- Subresource integrity (SRI) 

</div>
<hr>

<div>

##### browser sandbox
- javascript code running in the browser is restricted   
	- no local resources
		- no direct access to devices, files and local network
	- only browser APIs
		- limited access to resources allowed by the user
			- same origin only
			- code and data from different sites cannot interact

</div>
<hr>

##### node.js vs browser:
<br>

| Javascript in the browser        | Javascript in node.js    |
| -------------------------------- | ------------------------ | 
| downloaded from the web     | loaded from the local     |
| untrusted and highly restricted     | trusted and highly privileged     |
| limited blast radius     | may lead to server compromise     |

<br>

<div>

##### security pitfalls:
- dynamic type system 
	- abusing conversions and comparisons
	- automatic conversions
	- unexpected code may be executed
- loose comparisons
	- security checks may be bypassed
		- ***always use strict mode***
			 - ===
			- using Object.is
			- verify types of untrusted data items
- dynamic code execution
	- interpreting untrusted data as code
- prototypal inheritance
	- modifying behavior of child objects

<br>

### Examples

```
/*strict mode*/
if(typeof field !== 'string' || typeof value !== 'string') {
	res.sendStatus(400);
	return;
}
```

```
if (items[i][field] == value) {
	results.push(items[i]);
}
	/*prefer using === over ==, strict mode*/
	
if (items[i][field] === value) {
	results.push(items[i]);
}
```
		
</div>

<br>

</div>

<div>

## Preventing Code Injection Attacks

<hr style="border:3px solid grey">
<div>

##### Dynamic code execution:
- parse
	- transform source code into abstract syntax tree
- compile
	- generate bytecode just-in-time (JIT)
- execute
	- run bytecode instructions
- ***Javascript can generate and execute new code at runetime***

<br>

- unsafe functions:
	- eval
		- direct and indirect invocation
		- global and current scope
	- function constructor
		- invoke like a function
		- only global scope
- unsafe browser API:
	- setTimeout
	- setInterval
- prevent code injection
	- avoid unsafe functions
	- validate input
		- prefer allow lists over block lists
	- sanitize data passed to interpreters
	- apply principle of least authority
	- careful with third-party codes:
		- validate input data before passing them to libraries
	

</div>

</div>
<br>

<div>

## Defending against prototype pollution

<hr style="border:3px solid grey">

<div>

##### inheritance models:
- classes
	- static hierarchy of types
	- hierarchy doesn't change at code runtime
- prototypes
	- dynamic chain of objects
	- change during runtime
	- prototype chain
		- each object has a prototype
		- the chain ends with null (last object in chain)
		- inherited properties
		- only own properties are mutated
- safe solution:
	- validate JSON schema
			- Object.freeze
				- ***can freeze some libraries!***
	- create objects without prototype
		- Object.create(null, ...)
	- use *Map* instead of {} 

</div>

</div>

<br>

<div>

## Testing code

<hr style="border:3px solid grey">

<div>

##### Security testing tehniques:
- SAST
	- static application security testing
- DAST
	- dynamic application security testing
- IAST
	- interactive application security testing

<br>

| SAST                   |    DAST                        |
| ------------------ | ------------------------ |
| source code        | running application |
| known bad code patterns | malicious payloads |
| safe (only reads code) | may be destructive |
| compilers, linters, scanners | automated tests and scanners |
| ESLint | |
| Github code scanning and LGTM | |
| semgrep |  |

<br>

##### Using ESLint (SAST)
linters are lightweight code analysis tools that flag bugs and coding errors
- parse code and analyze the abstract syntax tree (AST)
- extensible -> comes with a set of bundled checks
- fast -> can be used by IDEs and build pipelines

<br>

Dependency management:
- ***detect vulnerable library with ```npm audit```***
- Retire.js
- Dependency-Track
- Snyk

</div>

</div>