# UC1: Create Project
### Actor: 
Team Member/Team Lead
### Precondition: 
User is logged in
### Trigger: 
User selects "Create Project"
### Main Flow:
1. User enters project details (title, description, due date)
2. System validates inputs.
3. System sends a message to the Kafka queue that a project should be persisted (async event)
4. Backend persists the project data in the relational database
5. Async confirmation is sent back to the messaging queue
6. Confirmation is shown to user.
### Postcondition: 
- Project is available for tasks to be created and other users to be added
- The user which created the project is assigned as the "team lead" for that project

# UC2: Create Task
### Actor: 
Team Member
### Precondition: 
User is logged in
### Trigger: 
User selects "Create Task"
### Main Flow:
1. User enters task details (project ID, title, description, due date, assignee)
2. System validates inputs.
3. System sends a message to the Kafka queue that a task should be persisted (async event)
4. Backend persists the task data in the relational database
5. Async confirmation is sent back to the messaging queue
6. Confirmation is shown to user.
### Postcondition: 
- Task is available under the project

# UC3: User Login
### Actor: 
Any user (team member, team leader, administrator)
### Precondition: 
User has been onboarded
### Trigger: 
User selects "Log in"
### Main Flow: 
1. User enters login credentials (username, password)
2. System (authentication microservice) validates login credentials (encrypted in transit)
3. Authentication microservice responds with JWT token if the login was successful 
4. System serves the user's home page 
5. System client side caches the JWT and session information
### Postcondition: 
- The user is logged in and has a live session
- A JWT was generated and is cached on the client side for easy and quick retrieval for subsequent requests
- The user's "home page" is displayed

# UC4: Search Project
### Actor: 
Team Member/Team Lead
### Precondition: 
User is logged in
### Trigger: 
User enters a project ID in the search and selects "Search"
### Main Flow: 
1. User enters a project ID
2. System validates the input
3. System sends a message to the kafka queue that a project search has been requested (async event) along with the user's session information (JWT)
4. Backend consumes the Kafka message
5. Backend searches the relational database for the project. 
6. Backend validates the user's JWT and performs an authorization check to ensure that the user is able to view the requested project
7. System serves the "view project" page via the messaging queue response 
### Postcondition: 
- The "view project" page is displayed with the requested project

# UC5: Add user to project
### Actor: 
Team Lead
### Precondition: 
- User is logged in
- A project is created
- The user to be added is created
### Trigger: 
User selects "add user"
### Main Flow: 
1. User searches for the project (reference: UC4)
2. User selects "add user" on the "view project" page
3. User enters the desired user's username and submits
4. System sends a message to the Kafka queue that an "add user" request was submitted (async event) along with the user's session information (JWT)
5. Backend (project microservice) consumes the Kafka message
6. System validates the session JWT
7. System associates the user with the project
8. System sends a response to the messaging queue
9. A confirmation is shown to the user
### Postcondition: 
- The user has been associated with the project

# UC6: Update Project Details
### Actor: 
Team Lead
### Precondition: 
- User is logged in
- A project is created
### Trigger: 
User selects "Project Settings"
### Main Flow: 
1. User searches for the project (reference: UC4)
2. User selects "Project Settings" on the "view project" page
3. The system validates the user's session and serves the "project settings" page (async event)
4. The user makes any updates which are needed and clicks "save"
5. The system validates the user's session and persists the updates
6. A confirmation is shown to the user
### Postcondition: 
- The desired project details have been changed

# UC7: Update Task Details
### Actor: 
Team Member/Team Lead
### Precondition: 
- User is logged in
- A project is created
- A task is created
- The user is a part of the project
### Trigger: 
User selects "Update" on the task
### Main Flow: 
1. User searches for the project (reference: UC4)
2. User selects "Update" on a task
3. The system validates the user's session and displays the "update task" screen (async event)
4. User update any required task details and selects "Save"
5. System validates the user's session and persists the changes (async event)
6. A confirmation is shown to the user
### Postcondition: 
- Task details have been changed

# UC8: New User Onboarding
### Actor: 
Unregistered user
### Precondition:
None
### Trigger: 
User selects "Create Account" 
### Main Flow: 
1. User selects "Create Account"
2. User enters personal details (username, password, email)
3. System persists the user details (async event)
4. A confirmation is shown to the user
5. User is directed back to the login page
### Postcondition: 
- A user is created