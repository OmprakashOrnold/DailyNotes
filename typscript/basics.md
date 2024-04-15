# TypeScript Notes


## TypeScript Installation

1) Install Node JS

2) Install TypeScript


   - Download Node JS installer from -> https://nodejs.org/en/download/

   - After installing Node, we can verify installation process by executing below command   in cmd

			node -v

   - Install TypeScript using below command

			npm install -g typescript

   - After installing TypeScript, we can verify installation using below command

			tsc -v
			


## TypeScript file has .ts extension 

## Code Running Steps


- Open command prompt and compile ts file

		tsc fileName.ts

    Note: **tsc compiler will convert ts file into js file (Transpilation)**

- Run JS file using below command

		node fileName.js



## 1 Example Hello World

	console.log("Hello World");
	
## 2 Example Define Variables

### Syntax for variables

	let <Varaible Name> : <type> =<inital value>

### Example
```typescript
	let found:boolean = true;
	let grade:number = 30;
	let firstName:string="Om Prakash";
	let lastName:string ="Peddamadthala";
	
	
	console.log(found);
	console.log("The Grade is +"+grade);
	console.log("Here this is my name "+firstName +" "+lastName);
	//string template
	console.log(`Here my name is ${firstName}  ${lastName}`);
```	
	
 ## 3 Example Loops And Array
```typescript
	let numberArray:number[]=[1,4,5,6,4,-3];
	 
	let addNumber:number =0;
	for(let i=0;i< numberArray.length ;i++){
	  addNumber=addNumber+numberArray[i];
	}
	console.log(addNumber)
```
