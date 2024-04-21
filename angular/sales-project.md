# Angular - Create New Component

## Our Goal
### Create a new Angular component to display a table of data

![Screenshot 2024-04-21 154318](https://github.com/OmprakashOrnold/DailyNotes/assets/36263846/8738cad9-1912-487c-bf33-dc230ac089dc)

## Development Process

1. Create a new project
2. Update main template page
3. Generate a new component
4. Add new component selector to app template page
5. Generate a SalesPerson class
6. In SalesPersonListComponent, create sample data
7. In sales-person-list template file, build HTML table by looping over data

## Step 1: Create a new project
      
      ng new sales-project


       cd sales-project 

## Step 2: Update main template page

![Screenshot 2024-04-21 155116](https://github.com/OmprakashOrnold/DailyNotes/assets/36263846/26493b2e-4de6-494b-b591-447943dedf83)

## Step 3: Generate a new component

        ng generate component sales-person-list

### About the Generated Files

- **sales-person-list.component.ts**: the component class
- **sales-person-list.component.html**: the component template HTML
- **sales-person-list.component.css**: the component private CSS
- **sales-person-list.component.spec.ts**: the unit test specifications
- **UPDATE src/app/app.module.ts**: Adds the component to the main application module

### Main Application Module

## Step 4: Add new component selector to app template page

![Screenshot 2024-04-21 155820](https://github.com/OmprakashOrnold/DailyNotes/assets/36263846/9186682d-071d-4d95-86d3-f7bba4250c03)

## Step 5: Generate a SalesPerson class

            ng generate class sales-person-list/SalesPerson

```typescript
            export class SalesPerson {

               constructor(public firstName:string,
                           public lastName:string,
                           public email:string,
                           public salesValume:number){
                
               }
```

}

![Screenshot 2024-04-21 155848](https://github.com/OmprakashOrnold/DailyNotes/assets/36263846/73c1d9b2-b5fe-453c-9f86-dd33cacdd924)
## Step 6: In SalesPersonListComponent, create sample data
![Screenshot 2024-04-21 165616](https://github.com/OmprakashOrnold/DailyNotes/assets/36263846/6b410a57-0e9b-4755-9cac-a01b07ed2e5d)


## Step 7: In sales-person-list template file, build HTML table by looping over data
```html
<table border="1">
    <thead>
        <tr>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Email</th>
            <th>Sales value</th>
        </tr>
    </thead>
    <tbody>
        <tr *ngFor="let tempSalesPerson of salesPersonList">
            <td>{{tempSalesPerson.firstName}}</td>
            <td>{{tempSalesPerson.lastName}}</td>
            <td>{{tempSalesPerson.email}}</td>
            <td>{{tempSalesPerson.salesValume}}</td>
        </tr>

    </tbody>
</table>

```
## ngFor 

- ngFor is a structural directive
• It renders a template for each item in a collection

