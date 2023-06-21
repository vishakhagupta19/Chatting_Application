# ChatApp  #

![](http://g.recordit.co/JYruQDLd0h.gif)

A small functional person-to-person message center application built using Django.
It has a REST API and uses WebSockets to notify clients of new messages and 
avoid polling.

## Architecture ##
-Upon user login, the frontend retrieves the user list and establishes a WebSocket connection to the server for receiving notifications.
-When a user selects another user for a chat, the frontend retrieves the most recent 15 messages exchanged between them.
-To send a message, the frontend sends a POST request to the REST API. Django, the backend framework, saves the message and uses the WebSocket connection to notify 
 the involved users by sending the ID of the new message.
-Upon receiving a notification about a new message (including the message ID), the frontend performs a GET request to the API to retrieve and download the received 
 message
 
### Database ###
For this demo, a straightforward MySQL configuration is being used. If greater performance is desired, it is possible to deploy a MySQL cluster or shard.
Please note that indexes are being employed to enhance performance in this context.

## Assumptions ##
Because of time constraints this project lacks of:

- User Sign-In / Forgot Password
- User Selector Pagination
- Good Test Coverage
- Better Comments / Documentation Strings
- Frontend Tests
- Modern Frontend Framework (like React)
- Frontend Package (automatic lintin, building and minification)
- Proper UX / UI design (looks plain bootstrap)

## Run ##

0. move to project root folder


1. Create and activate a virtualenv (Python 3)
```bash
pipenv --python 3 shell
```
2. Install requirements
```bash
pipenv install
```
3. Create a MySQL database
```sql
CREATE DATABASE chat CHARACTER SET utf8;
```
4. Start Redis Server
```bash
redis-server
```

5. Init database
```bash
./manage.py migrate
```
6. Run tests
```bash
./manage.py test
```

7. Create admin user
```bash
./manage.py createsuperuser
```

8. Run development server
```bash
./manage.py runserver
```

To override default settings, create a local_settings.py file in the chat folder.


MESSAGES_TO_LOAD = 15
```
