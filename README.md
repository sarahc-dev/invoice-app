# Invoice App

A full-stack invoice management app based on this 
[Frontend Mentor challenge](https://www.frontendmentor.io/challenges/invoice-app-i7KaLTQjl). I wanted to create a larger portfolio project and keep learning. So I am going to 
build this with Java Spring Boot and a SQL database on the backend and React on the frontend. In addition, I am going to 
add user authentication to learn about this in Java. I am also dipping my toes into AWS and hoping to deploy this. 

## Built with

- Java
- Spring Boot
- Gradle
- React
- Figma (Design file provided by Frontend Mentor)

## The Challenge

![app preview](./images/preview.jpg)

Users should be able to:

- View the optimal layout for the app depending on their device's screen size
- See hover states for all interactive elements on the page
- Create, read, update, and delete invoices
- Receive form validations when trying to create/edit an invoice
- Save draft invoices, and mark pending invoices as paid
- Filter invoices by status (draft/pending/paid)
- Toggle light and dark mode
- Keep track of any changes, even after refreshing the browser

Expected Behaviour

- Creating an invoice
    - When creating a new invoice, an ID needs to be created. Each ID should be 2 random upper-cased letters followed by 4 random numbers.
    - Invoices can be created either as drafts or as pending. Clicking "Save as Draft" should allow the user to leave any form field blank, but should create an ID if one doesn't exist and set the status to "draft". Clicking "Save & Send" should require all forms fields to be filled in, and should set the status to "pending".
    - Changing the Payments Terms field should set the `paymentDue` property based on the `createdAt` date plus the numbers of days set for the payment terms.
    - The `total` should be the sum of all items on the invoice.
- Editing an invoice
    - When saving changes to an invoice, all fields are required when the "Save Changes" button is clicked. If the user clicks "Cancel", any unsaved changes should be reset.
    - If the invoice being edited is a "draft", the status needs to be updated to "pending" when the "Save Changes" button is clicked. All fields are required at this stage.
- Users should be able to mark invoices as paid by clicking the "Mark as Paid" button. This should change the invoice's status to "paid".
- Users should receive a confirmation modal when trying to delete invoices.

## Planning

### API routes

| HTTP verb | API endpoint  | Purpose               |
|-----------|---------------|-----------------------|
| GET       | /invoices     | Gets all invoices     | 
| POST      | /invoices     | Add a new invoice     |
| GET       | /invoices/:id | Gets a single invoice |
| PUT       | /invoices/:id | Edits an invoice      |
| PATCH     | /invoices/:id | Edits invoice status  |
| DELETE    | /invoices/:id | Deletes an invoice    |

I'm going to start by building the app without user authentication and add this in later. In my app I need a list of all invoices and the details of individual invoices. I considered whether to have one API 
route that returns all invoices (with all data) and manage this client side by passing individual invoices as props. Or 
whether to get individual invoices by through another request. I decided on the second option, firstly because there is
a lot of fields in the invoice - so I would initially be getting more data than is necessary especially if there was
a lot of invoices. Also, the invoice contains an items list. As I am using SQL I think this is going to be a separate 
table, so it feels more appropriate to fetch the joined data per invoice. I also decided to make a separate PUT and 
PATCH request based on the design file. The edit invoice screen is the whole form - so I have access to all the data and
to ensure consistency I think is better to replace the item with the edited one. Whereas updating the status is a button 
click to update a single field - so a PATCH request seems more appropriate.