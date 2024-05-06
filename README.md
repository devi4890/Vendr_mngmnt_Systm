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
# Testing or Using the API endpoints.
- we can test API endpoints using curl or httpie commands. 
## Create a vendor:
### using curl:
- curl -H "Authorization: Token your_obtained_token" -X POST http://127.0.0.1:8000/api/vendors/ -d "vendor_code=01&name=Vendor+1&contact_details=Contact+1&address=Address+1"
### using httpie:
- http POST http://127.0.0.1:8000/api/vendors/ 
### About this API endpoint:
- here this endpoint is used to create a vendor by providing the vendor details.
## List all Vendors details:
### using curl:
- curl -H "Authorization: Token your_obtained_token" http://127.0.0.1:8000/api/vendors/
### using httpie:
- http http://127.0.0.1:8000/api/vendors/ "Authorization: Token your_obtained_token"
### About this API endpoint:
- here this endpoint is used to get the details of all vendors.
## Retrieve a specific vendor's details:
### using curl:
- curl -H "Authorization: Token your_obtained_token" http://127.0.0.1:8000/api/vendors/{vendor_id}/
### using httpie:
- http http://127.0.0.1:8000/api/vendors/{vendor_id}/ 
### About this API endpoint:
- here this endpoint is used to get the details of vendor with vendor_id which was mentioned in the command. 
## Update a vendor's details:
### using curl:
#### PUT method:
- curl -H "Authorization: Token your_obtained_token" -X PUT http://127.0.0.1:8000/api/vendors/{vendor_id}/ -d "vendor_code=updated code&name=Updated Vendor Name&contact_details=Updated Contact Details&address=Updated Address"
#### PATCH method:
- curl -H "Authorization: Token your_obtained_token" -X PATCH http://127.0.0.1:8000/api/vendors/{vendor_id}/ -d "name=Updated Vendor Name"
### using httpie:
#### PUT method:
- http PUT http://127.0.0.1:8000/api/vendors/{vendor_id}/ vendor_code="updated vendor code" name="Updated Vendor Name" contact_details="Updated Contact Details" address="Updated Address" "Authorization: Token your_obtained_token"
#### PATCH method:
- http PATCH http://127.0.0.1:8000/api/vendors/{vendor_id}/ name="Updated Vendor Name" contact_details="Updated Contact Details" address="Updated Address" "Authorization: Token your_obtained_token"
### About this API endpoint:
- here this endpoint we have two commands with different http methods (PUT,PATCH).As we have a primary key in the model the PUT method works as POST method (which means it creates a new vendor with given details). The PATCH method is used to update the vendor's details except vendor's id. here PUT handles updates by replacing the entire entity, so it creates a new entity. but where the PATCH handles by only updating the given fields.
## Delete a vendor:
### using curl:
- curl -H "Authorization: Token your_obtained_token" -X DELETE http://127.0.0.1:8000/api/vendors/{vendor_id}/
### using httpie:
- http DELETE http://127.0.0.1:8000/api/vendors/{vendor_id}/
### About this API endpoint:
- here this endpoint is used to delete the vendor with given vendor_id.

## Create a purchase_order:
### using curl:
- curl -H "Authorization: Token your_obtained_token" -X POST http://127.0.0.1:8000/api/purchase_orders/ -d "po_number=01&vendor=01&order_date=2023-01-01T12:00:00&delivery_date=2023-01-10T12:00:00&items=[{\"item_name\":\"Item 1\",\"quantity\": 10 },{\"item_name\":\"Item 2\",\"quantity\": 10 }]&quality_rating=4.5&issue_date=2023-01-01T12:00:00&status=updated&acknowledgment_date=2023-01-02T12:00:00"
- curl -H "Authorization: Token your_obtained_token" -X POST http://127.0.0.1:8000/api/purchase_orders/ -d "po_number=01&vendor=01&order_date=2023-01-01T12:00:00&delivery_date=2023-01-10T12:00:00&items=[{\"item_name\":\"Item 1\",\"quantity\": 10 },{\"item_name\": 10 }]&quality_rating=4.5&issue_date=2023-01-01T12:00:00&status=updated&acknowledgment_date=2023-01-02T12:00:00"
### using httpie:
- http POST http://127.0.0.1:8000/api/purchase_orders/ po_number="01" vendor=01 order_date="2023-01-01" delivery_date="2023-01-10" items='[{"item_name": 20 }]' quality_rating=4.5 issue_date="2023-01-01" status="Pending" acknowledgment_date="2023-01-02" "Authorization: Token your_obtained_token"
### About this API endpoint:
@@ -118,7 +118,7 @@ Open the Django admin at http://127.0.0.1:8000/admin/ and log in using the super
## Update a purchase_order's details:
### using curl:
#### PUT method:
- curl -H "Authorization: Token your_obtained_token" -X PUT http://127.0.0.1:8000/api/purchase_orders/{po_id}/ -d "po_number=updatedno&vendor=updatedvno&order_date=2023-01-02T12:00:00&delivery_date=2023-01-15T12:00:00&items=[{\"item_name\":\"updated item 2\",\"quantity\": 10 },{\"item_name\":\"updated Item 2\",\"quantity\": 10 }]&quality_rating=5&issue_date=2023-01-01T12:00:00&status=updated&acknowledgment_date=2023-01-01T12:00:00"
- curl -H "Authorization: Token your_obtained_token" -X PUT http://127.0.0.1:8000/api/purchase_orders/{po_id}/ -d "po_number=updatedno&vendor=updatedvno&order_date=2023-01-02T12:00:00&delivery_date=2023-01-15T12:00:00&items=[{\"item_name\": 10 },{\"item_name\":10}]&quality_rating=5&issue_date=2023-01-01T12:00:00&status=updated&acknowledgment_date=2023-01-01T12:00:00"
#### PATCH method:
- curl -H "Authorization: Token your_obtained_token" -X PATCH http://127.0.0.1:8000/api/purchase_orders/{po_id}/ -d "vendor=updatedvno&quality_rating=5"
### using httpie:
@@ -127,7 +127,7 @@ Open the Django admin at http://127.0.0.1:8000/admin/ and log in using the super
#### PATCH method:
- http PATCH http://127.0.0.1:8000/api/purchase_orders/{po_id}/ order_date="2023-01-02T12:00:00" delivery_date="2023-01-15T12:00:00" items:='[{"item_name": "Updated Item", "quantity": 20 }]' quality_rating:=4.8 status="updated" "Authorization: Token your_obtained_token"
### About this API endpoint:
- here this endpoint we have two commands with different http methods (PUT,PATCH).As we have a primary key in the model the PUT method works as POST method (which means it creates a new purchase_order with given details). The PATCH method is used to update the purchase_order's details except purchase_order's number. here PUT handles updates by replacing the entire entity, so it creates a new entity. but where the PATCH handles by only updating the given fields.
- here this endpoint we have two commands with different http methods (PUT,PATCH).As we have a primary key in the model the PUT method works as POST method (which means it creates a new purchase_order with given details). The PATCH method is used to update the purchase_order's details except purchase_order's number. here PUT handles updates by replacing the entire entity, so it creates a new entity. but where the PATCH handles by only updating the given fields.(we can provide any no of fields in PATCH mathod.)

## Delete a purchase_order:
### using curl:
@@ -151,9 +151,9 @@ Open the Django admin at http://127.0.0.1:8000/admin/ and log in using the super

## Update acknowledgment_data and trigger the recalculation of average_response_time:
### using curl:
- curl -H "Authorization: Token your_obtained_token" -X POST http://127.0.0.1:8000/api/purchase_orders/{po_id}/acknowledge/
- curl -H "Authorization: Token your_obtained_token" -X PATCH http://127.0.0.1:8000/api/purchase_orders/{po_id}/acknowledge/ --data "acknowledgment_date=2023-12-30T12:00:00Z"
### using httpie:
- http POST http://127.0.0.1:8000/api/purchase_orders/{po_id}/acknowledge/ 
- http PATCH http://127.0.0.1:8000/api/purchase_orders/{po_id}/acknowledge/ Authorization: Token your_obtained_token" acknowledgment_date="2023-12-20T12:00:00Z"
### About this API endpoint:
- here this endpoint is used to acknowledge the purchase_order with given po_id and trigger the recalculation of average_reponse_time.
