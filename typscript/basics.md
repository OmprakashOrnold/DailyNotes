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

## NOTE 1 :- If an error occurs version issue run below command (Flags)
	
	sc --target ES5 --noEmitOnError  Customer.ts

## NOTE 2 :- To Generate tsConfig file (Instead of Flags use config file)

	tsc --init

## 9 Example Short Cut Constructor
```typescript
	class CustomerWork {
	
	    constructor( private _firstName:string, private _lastName:string){
	       
	    }
	
	public get firstName():string{
	    return this._firstName;
	}
	
	public get lastName():string{
	    return this._lastName;
	}
	    
	}
	
	//lets create instance
	let customerWork =new CustomerWork("Prakash","aaasd");
	
	console.log(customerWork.firstName+" "+customerWork.lastName)
```
## TypeScript Modules

+ TypeScript supports the concept of modules

+ A module can **export** classes ,functions , variables etc..,

+ Another file can **import** classes ,functions, variables etc..,from a module

## 10 Example Modules Export and Import

### Example Export
```typescript
	export class CustomerNew {
	
	    constructor( private _firstName:string, private _lastName:string){
	    }
	
	public get firstName():string{
	    return this._firstName;
	}
	
	public get lastName():string{
	    return this._lastName;
	}
	    
	}
```	
### Example Import
```typescript
	import { CustomerNew } from "./CustomerNew";
	
	let customerNew =new CustomerNew("Rakesh","Peddamadthala");
	
	console.log(customerNew.firstName);
	console.log(customerNew.lastName);
```

## Example Inheritance

### Shape.ts
```typescript
	export class Shape{
	    constructor( private _x:number,private _y:number){
	    }
	
	    public get x(){
	        return this._x;
	    }
	    public set x(value:number){
	         this._x=value;
	    }
	    
	    public get y(){
	        return this._y;
	    }
	
	    public set y(value:number){
	         this._y=value;
	    }
	    
	    getInfo():string{
	        return  `x=${this._x} ,y=${this._y}`
	    }
	}
	
```
### Circle.ts
```typescript	
	import { Shape } from "./Shape";
	
	export class Circle extends Shape{
	
	    constructor(theX:number,theY:number, private _radius:number){
	         super(theX,theY);
	    }
	
	    public get radius(){
	         return this._radius;
	    }
	
	    public set radius(value:number){
	        this._radius=value;
	    }
	
	     public getInfo(): string {
	        return super.getInfo()+` radius=${this._radius} `
	    }
	}
```
### Rectangle.ts
```typescript
	import { Shape } from "./Shape";
	
	export class Rectangle extends Shape{
	
	
	    constructor(theX:number,theY:number, private _width:number, private     _length:number){
	        super(theX,theY)
	    }
	    
	    public get width(){
	        return this._width;
	    };
	
	    public set width(value:number){
	        this._width=value;
	    }
	
	    public get length(){
	        return this._length;
	    };
	
	    public set length(value:number){
	        this._length=value;
	    }
	
	     public getInfo(): string {
	        return super.getInfo()+` width =${this._width} , length = ${this._length}`
	    }
	
	}
```
### Driver.ts
```typescript
	import { Shape } from "./Shape";
	import { Circle } from "./Circle";
	import { Rectangle } from "./Rectangle";
	
	//lets create instnce
	let myShape =new Shape(23,7);
	console.log(myShape.getInfo());
	
	let myCircle = new Circle(5,5,8.5);
	console.log(myCircle.getInfo())
	
	let myRectangle =new Rectangle(0,0,2,4);
	console.log(myRectangle.getInfo())
```	

### ArrayDriver.ts
```typescript
import { Shape } from "./Shape";
import { Circle } from "./Circle";
import { Rectangle } from "./Rectangle";

//lets create instnce
let myShape =new Shape(23,7);
let myCircle = new Circle(5,5,8.5);
let myRectangle =new Rectangle(0,0,2,4);

let theShapes:Shape[]= [];

theShapes.push(myShape);
theShapes.push(myCircle);
theShapes.push(myRectangle);


for(let theShape of theShapes){
    console.log(theShape.getInfo())
}
```
