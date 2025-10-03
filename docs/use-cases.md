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

# UC4: Search Project

# UC5: View Project

# UC6: Add user to project

# UC7: Update Project Details

# UC8: Update Task Details

# UC9: New User Onboarding