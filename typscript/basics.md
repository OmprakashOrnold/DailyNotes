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
```typescript	
 ## 3 Example Loops And Array

	let numberArray:number[]=[1,4,5,6,4,-3];
	 
	let addNumber:number =0;
	for(let i=0;i< numberArray.length ;i++){
	  addNumber=addNumber+numberArray[i];
	}
	console.log(addNumber)

## 4 Example Simplified Loop
```typescript
	let sportsOne:string[] =["Golf","Football","Cricket","Swimming"];
	
	for(let tempSport of sportsOne){
	    if(tempSport=="Cricket"){
	        console.log(tempSport+">>> is my favorite")
	    }else{
	        console.log(tempSport)
	    }
	}
```
## 5 Example Growable Array
```typescript
	let games:string[]=["Carram","Chess","tennies","Football"];
	
	games.push("Vooley Ball");
	games.push("Circket Ball")
	
	
	for(let game of games){
	    console.log(game);
	}
```
## 6 Example Define Class

### Basic Structure
```typescript
	class Customer {
	    // properties
	    // constructors
	    // getter / setter methods
	}
```
### Example Class
```typescript
	class Customer{
	    
	    firstName : string;
	    lastName : string;
	  
	}
	//lets create customer instance
	let customer= new Customer();
	
	customer.firstName="Om Prakash";
	customer.lastName="Peddamadthala";
	
	console.log(customer.firstName);
	console.log(customer.lastName);
```	
## 7 Example Define Class And Constructor
```typescript
	class Customer{
	
	    firstName : string;
	    lastName : string;
	  
	    constructor(theFirst:string,theLast:string){
	        this.firstName=theFirst;
	        this.lastName=theLast
	    }
	}
	//lets create customer instance
	let customer= new Customer("Om Prakash","Peddamadthala");
	
	
	console.log(customer.firstName);
	console.log(customer.lastName);
```	

## 8 Example Getter & Setter For Class

### Access Modifiers
        
- **public**   Property is accessible to all classes (default modifier

- **private**  Property is only accessible in current class and subclasses

- **protected** Property is only accessible in current class

### Example
```typescript
		class Customer{
		    
		private _firstName : string;
		private _lastName : string;
		  
		    constructor(theFirst:string,theLast:string){
		        this._firstName=theFirst;
		        this._lastName=theLast
		    }
		
		    public get firstName():string{
		        return this._firstName;
		    }
		
		    public get lastName():string{
		        return this._lastName;
		    }
		
		
		}
		//lets create customer instance
		let customer= new Customer("Om Prakash","Peddamadthala");
		
		
		
		console.log(customer.firstName);
		console.log(customer.lastName);
```
