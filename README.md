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
- Update the page and redirect (E.x.: "/home")

### Sign Up

- Name, Email and Password required. 
- If Email already exists, return message warning.
- Password requires at least 1 uppercase letter, 1 lowcase letter and 1 special character, minimum 8 characters.
- Validate password on frontend and backend for more safety.
- IF OK, POST the new data on the database and redirect (E.x.: "/dashboard")
- IF NOT, display the respective error message

### Frontend 

- Download assets (images) 
- Declare variables colors (E.x. --dark_gray, --black, --white)
- Create a comment for each section (E.x.: Navbar, Dashboard, profile)
- Development screen order: 
  1. Phone
  2. Tablet
  3. Laptop
  4. Desktop 
- Form input validations using regular expressions (REGEX) (E.x.: If the password doesn't have 12+ characters and an uppercase letter, lowercase letter... return error!)
  
  #### API
   - Login: POST request to backend authenticate user, example:
        ```js
         async function Login(){
        
          await fetch("https://url-api/login", {
              method: 'POST'
              headers: {
                content: "application/json"
              },
              body: JSON.stringify({
              email: emailInput.value,
              password: passwordInput.value
              })
        
          }).then(res => {
              if(!res.ok){
              throw new Error('Error to login!')
            }
            return res.json
        
          }).then(data => {
            localStorage.setItem('authenticateToken', data.token) // Save token to validate user on the local storage
            window.location.href = "/dashboard" // Redirect to dashboard page
          
          }).catch(error => {
              console.error(error)
            })
        
        }
        ```
  - Logout: Delete the reference that is saved in the browser, example:
    ```js
    function Logout() {
        localStorage.remove('authenticateToken')
        window.location.href = "/login" // Redirects to 'Login' page
    }
    ```
  - SignUp: Send the input values to backend validate it, example:
    ```js
    function SignUp() {
    
      await fetch("https://url-api/signup", {
              method: 'POST'
              headers: {
                content: application/json
              },
              body: JSON.stringify({ // Take the data from the user's form and send in the body as a request
              name: nameInput.value,
              email: emailInput.value,
              password: passwordInput.value,
              confirmPassword: confirmPasswordInput.value
              })
        
          }).then(res => {
              if(!res.ok){
                window.alert('Error to Singup, verify the credentials!') // Error Message
                return
              }
             return res.json
             })

            .then(() => {
                window.alert("Account created! Please Login.") // Successful message
                window.location.href = "/login" // Redirect To Login
              })
    
            .catch(error => {
              console.error(error)
             });
    
    }
    ```
  - Page:
      - Adding: When the user click on the button to add a new page, he gonna gonna display the following function:
          ```js
            function addPage(newPageData) {
          
              const baseUrl = 'https://api.example.com'; 
              const url = `${baseUrl}/cms/pages`; // Endpoint for creating pages
              const headers = {
                'Content-Type': 'application/json'
              };
              const requestOptions = {
                method: 'POST',
                headers: headers,
                body: JSON.stringify(newPageData)
              };
            
              return fetch(url, requestOptions)
                .then(response => {
                  if (!response.ok) { 
                    throw new Error('Error creating new page: ' + response.status); // If response won't be ok, it gonna throw an error
                  }
                  return response.json();
                })
                .then(data => {
                  window.alert('New page created successfully:', data); // Alert the user that the page was added successfully
                })
                .catch(error => {
                  console.error('Error creating new page:', error.message); // Display error message in case of an API error
                  throw error;
                });
          
            }
          ```
        - Editing: The edit logic is similar to adding a new page, but instead of using 'POST' method (create a new request), we gonna use 'PUT' method (edit a request that already exists), example:
           ```js
             function editPage(pageId, updatedPageData) { // Necessary to specify the pageID to edit the requested page
              const baseUrl = 'https://api.example.com'; 
              const url = `${baseUrl}/cms/pages/${pageId}`; // Endpoint for editing a page
              const headers = {
                'Content-Type': 'application/json'
              };
              const requestOptions = {
                method: 'PUT',
                headers: headers,
                body: JSON.stringify(updatedPageData)
              };
            
              return fetch(url, requestOptions)
                .then(response => {
                  if (!response.ok) {
                    throw new Error('Error editing page: ' + response.status); // Error message displayed if there is some wrong request
                  }
                  window.alert('Page edited successfully.'); // Show to the user that the page was edited if the response is OK
                })
                .catch(error => {
                  window.alert('Error editing page:', error.message); // If there is some error on API request, display the error.
                  throw error;
                });
            }
           ```
        - Deleting: To delete a page it gonna be necessary only the pageID to specify which page it will be deleted, example:
          ```js
          function deletePage(pageId) {
              const baseUrl = 'https://api.example.com';
              const url = `${baseUrl}/cms/pages/${pageId}`; // Endpoint for deleting a page
              const requestOptions = {
                method: 'DELETE'
              };
            
              return fetch(url, requestOptions)
                .then(response => {
                  if (!response.ok) {
                    window.alert('Error deleting page: ' + response.status); // Tell the user that there was some error on deleting the page
                    return
                  }
                  window.alert('Page deleted successfully.'); // Show to the user the message was successfully deleted
                })
                .catch(error => {
                  window.alert('Error deleting page:', error.message);  // If there is some error on API request, display the error.
                  throw error;
                });
            }
 
