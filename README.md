# CMS-Logic-Implementation


## Project Initialized

- Install the dependencies (I.e.: "ng add @angular/pwa", "npm install @rx-angular/isr"...) ;
- Split the responsibilities in different filles (I.e.: [styles], [components], [context], [API], [assets]) ;
- Classes for authentication (I.e.: Class ADMIN {permission: "ADMIN"}) ;

### Access Validation:

- Is user Logged? Validate User.
- IF validated, permit access. IF not, redirect (E.x.: "/home")

### Login:

- Take the data from the login
- Send a request to BACKEND validate these data on DataBase
- IF OK, save a reference (token) on user's Browser (I.e.: ADD Cookie or LocalStorage or Cache...) and redirect (E.x.: "/dashboard")
- IF NOT, just show error message.

### Logout:

- DELETE reference that is in the browser (I.e.: REMOVE Cookie or LocalStorage or Cache...)
- Send a request to backend to DELETE the reference in DB (E.x.: When using JWT.)
- Update the page and redirect (E.x.: "/home")

### Sign Up

- Name, Email and Password required. 
- If Email already exists, return message warning.
- Password requires at least 1 uppercase letter, 1 lowcase letter and 1 special character, minimum 8 characters.
- Validate password on frontend and backend for more safety.
- IF OK, save the new data on the database and redirect (E.x.: "/dashboard")
- IF NOT, display the respective error message
