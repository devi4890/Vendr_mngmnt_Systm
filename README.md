# Django REST API Setup
This repository contains a Django project with a RESTful API using Django REST Framework.
## Prerequisites
- Python (version 3.x recommended)
- Django
- Django REST Framework
# Setup Instructions
## Create a Virtual Environment:
- pip install virtualenvwrapper-win
- mkvirualenv environmentname
## Install Dependencies:
- pip install django
- pip install djangorestframework
## Set up a new project with a single application
- django-admin startproject Vendr_mngmnt_Systm                 
- cd Vendr_mngmnt_Systm
- django-admin startapp Vendors             
## Database migration                    
- python manage.py makemigrations      
- python manage.py migrate
## Superuser creation and Token generation
- python manage.py createsuperuser
- curl -X POST -d "username=your_superuser_username&password=your_superuser_password" http://localhost:8000/api-token-auth/
## Running the server
- python manage.py runserver
## Access Django Admin:
Open the Django admin at http://127.0.0.1:8000/admin/ and log in using the superuser credentials. this is to access the database as a admin user.
## how to run a api endpoint:
- first we need to make sure that we migrated the models to database
- then we need to start the server using "python manage.py runserver" command.
- then we need to open another cmd prompt and open virtual environment and open the project folder and provide curl or httpie commands.
- another way is open postman in VSCode only after opening and running the project in terminal.
# Testing or Using the API endpoints.
- we can test API endpoints using curl or httpie commands.
## User Login:
### using Postman:
-http://127.0.0.1:8000/auth/login
### About this API endpoint:
- here this endpoint is used to login a user by providing the user details.
## Token generating
-http://127.0.0.1:8000/api-token-auth/
### About this API endpoint:
Token will generate by applying the above api with username and password using POST method.
  
## Create a vendor:
### using Postman:
-http://127.0.0.1:8000/api/vendors/ 
-by using above api endpoint in postman first in headers add "Authorization" as key and "Token your_obtained_token" as value.please enter the obtained Token in the place of "Your_obtained_token" and use POST method enter the data in json format and send.Then we can create a vendor.
### using curl:
- curl -H "Authorization: Token your_obtained_token" -X POST http://127.0.0.1:8000/api/vendors/ -d "vendor_code=01&name=Vendor+1&contact_details=Contact+1&address=Address+1"
### using httpie:
- http POST http://127.0.0.1:8000/api/vendors/ 
### About this API endpoint:
- here this endpoint is used to create a vendor by providing the vendor details.
## List all Vendors details:
### using Postman:
-http://127.0.0.1:8000/api/vendors/
by using above api endpoint in postman first in headers add "Authorization" as key and "Token your_obtained_token" as value.please enter the obtained Token in the place of "Your_obtained_token" and use GET method and send.Then we can get the list of  vendors.
### using curl:
- curl -H "Authorization: Token your_obtained_token" http://127.0.0.1:8000/api/vendors/
### using httpie:
- http http://127.0.0.1:8000/api/vendors/ "Authorization: Token your_obtained_token"
### About this API endpoint:
- here this endpoint is used to get the details of all vendors.
## Retrieve a specific vendor's details:
### using Postman:
-http://127.0.0.1:8000/api/vendors/{vendor_id}/ 
### using curl:
- curl -H "Authorization: Token your_obtained_token" http://127.0.0.1:8000/api/vendors/{vendor_id}/
### using httpie:
-  http://127.0.0.1:8000/api/vendors/{vendor_id}/ 
### About this API endpoint:
- here this endpoint is used to get the details of vendor with vendor_id which was mentioned in the command. 
## Update a vendor's details:
###using postman:
-http://127.0.0.1:8000/api/vendors/{vendor_id}/
By putting authorization and token  in headers also add "Content-Type" and "application/json" as value.Using PUT method we can edit the vendor details.
### using curl:
#### PUT method:
- curl -H "Authorization: Token your_obtained_token" -X PUT http://127.0.0.1:8000/api/vendors/{vendor_id}/ -d "vendor_code=updated code&name=Updated Vendor Name&contact_details=Updated Contact Details&address=Updated Address"
### using httpie:
#### PUT method:
- http PUT http://127.0.0.1:8000/api/vendors/{vendor_id}/ vendor_code="updated vendor code" name="Updated Vendor Name" contact_details="Updated Contact Details" address="Updated Address".

## Delete a vendor:
### using postman:
- http DELETE http://127.0.0.1:8000/api/vendors/{vendor_id}/
### using curl:
- curl -H "Authorization: Token your_obtained_token" -X DELETE http://127.0.0.1:8000/api/vendors/{vendor_id}/
### using httpie:
- http DELETE http://127.0.0.1:8000/api/vendors/{vendor_id}/
### About this API endpoint:
- here this endpoint is used to delete the vendor with given vendor_id.

## Create a purchase_order:
### using postman:
-http://127.0.0.1:8000/api/purchase_orders/ 
-by using above api endpoint in postman first in headers add "Authorization" as key and "Token your_obtained_token" as value.please enter the obtained Token in the place of "Your_obtained_token" and use POST method enter the data in json format and send.Then we can create a purchase order.
### using curl:
- curl -H "Authorization: Token your_obtained_token" -X POST http://127.0.0.1:8000/api/purchase_orders/ -d "po_number=PO-003&vendor=3&order_date=2023-01-01T12:00:00&delivery_date=2023-01-10T12:00:00&items=[{\"item_name\":\"Item 1\",\"quantity\": 10 },{\"item_name\": 10 }]&quality_rating=4.5&issue_date=2023-01-01T12:00:00&status=updated&acknowledgment_date=2023-01-02T12:00:00"
### using httpie:
- http POST http://127.0.0.1:8000/api/purchase_orders/ po_number="PO-003" vendor=1 order_date="2023-01-01" delivery_date="2023-01-10" items='[{"item_name": 20 }]' quality_rating=4.5 issue_date="2023-01-01" status="Pending" acknowledgment_date="2023-01-02" "Authorization: Token your_obtained_token"
### About this API endpoint:
@@ -118,7 +118,7 @@ Open the Django admin at http://127.0.0.1:8000/admin/ and log in using the super
## Update a purchase_order's details:
### using postman:
-http://127.0.0.1:8000/api/purchase_orders/{po_id}/
By putting authorization and token  in headers also add "Content-Type" and "application/json" as value.Using PUT method we can edit the vendor details.
### using curl:
#### PUT method:
- curl -H "Authorization: Token your_obtained_token" -X PUT http://127.0.0.1:8000/api/purchase_orders/{po_id}/ -d "po_number=updatedno&vendor=updatedvno&order_date=2023-01-02T12:00:00&delivery_date=2023-01-15T12:00:00&items=[{\"item_name\":\"updated item 2\",\"quantity\": 10 },{\"item_name\":\"updated Item 2\",\"quantity\": 10 }]&quality_rating=5&issue_date=2023-01-01T12:00:00&status=updated&acknowledgment_date=2023-01-01T12:00:00"
- curl -H "Authorization: Token your_obtained_token" -X PUT http://127.0.0.1:8000/api/purchase_orders/{po_id}/ -d "po_number=updatedno&vendor=updatedvno&order_date=2023-01-02T12:00:00&delivery_date=2023-01-15T12:00:00&items=[{\"item_name\": 10 },{\"item_name\":10}]&quality_rating=5&issue_date=2023-01-01T12:00:00&status=updated&acknowledgment_date=2023-01-01T12:00:00"
### About this API endpoint:
-  The PUT method is used to update the purchase_order's details except purchase_order's number. here PUT handles updates by replacing the entire entity, so it creates a new entity.

## Delete a purchase_order:
### using postman:
-http://127.0.0.1:8000/api/purchase_orders/{po_id}/
### using curl:
-http://127.0.0.1:8000/api/purchase_orders/{po_id}/
@@ -151,9 +151,9 @@ Open the Django admin at http://127.0.0.1:8000/admin/ and log in using the super
## Performace data of vendor
### using httpie:
- http POST http://127.0.0.1:8000/api/vendors/{vendor_id}/performance/ 
### About this API endpoint:
- here this endpoint is used to acknowledge the vendor with given vendor_id 
## Update acknowledgment_data and trigger the recalculation of average_response_time:
### using curl:
- curl -H "Authorization: Token your_obtained_token" -X POST http://127.0.0.1:8000/api/purchase_orders/{po_id}/acknowledge/
- curl -H "Authorization: Token your_obtained_token" -X PATCH http://127.0.0.1:8000/api/purchase_orders/{po_id}/acknowledge/ 
### using httpie:
- http POST http://127.0.0.1:8000/api/purchase_orders/{po_id}/acknowledge/ 
### About this API endpoint:
- here this endpoint is used to acknowledge the purchase_order with given po_id and trigger the recalculation of average_reponse_time.
