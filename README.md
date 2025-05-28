# post-install-config
This tutorial outlines the post-install configuration of the open-source help desk ticketing system osTicket.

# osTicket - Post-Install Configuration

This tutorial outlines the post-install configuration of the open-source help desk ticketing system osTicket.

## Environments and Technologies Used
* Microsoft Azure (Virtual Machines/Compute)
* Remote Desktop
* Internet Information Services (IIS)

## Operating Systems Used
* Windows 10 (21H2)

## Post-Install Configuration Objectives
* Configure Roles, Departments, and Teams
* Allow anyone to create tickets
* Configure Agents (workers) and Users (customers)
* Configure SLA (Service Level Agreements)
* Configure Help Topics

## Configuration Steps

### Step 1: Access osTicket Admin Panel
- Navigate to your osTicket admin panel: http://localhost/osTicket/scp/login.php
- Log in with the admin credentials you created during installation
- You should now see the osTicket Admin Panel dashboard

### Step 2: Configure Roles
Roles determine the permissions that agents have within the help desk.

- Click Admin Panel → Agents → Roles
- Click "Add New Role"
- Create a "Supreme Admin" role:
  - Name: Supreme Admin
  - Under Permissions tab, check all boxes for:
    - Tickets (all permissions)
    - Tasks (all permissions) 
    - Knowledgebase (all permissions)
  - Under Teams tab, check "Assign/Close"
  - Click "Add Role"

### Step 3: Configure Departments
Departments are used to route tickets and assign agents.

- Click Admin Panel → Agents → Departments
- Note the default "Support" department exists
- Click "Add New Department"
- Create "System Administrators" department:
  - Name: System Administrators
  - Status: Active
  - Type: Public
  - SLA Plan: (leave default for now)
  - Manager: (assign yourself as manager)
  - Click "Create Dept"

### Step 4: Configure Teams
Teams allow you to group agents from different departments.

- Click Admin Panel → Agents → Teams
- Note "Level I Support" team already exists
- Click "Add New Team"
- Create "Level II Support" team:
  - Name: Level II Support
  - Status: Active
  - Lead: (assign yourself or another agent)
  - Click "Create Team"

### Step 5: Allow Anyone to Create Tickets
This setting enables unregistered users to submit tickets.

- Click Admin Panel → Settings → User Settings
- Under Authentication Settings:
  - Registration Required: UNCHECK this box
  - Registration Method: Public
- Under General Settings:
  - Guest Tickets: ENABLE this option
- Click "Save Changes"

### Step 6: Configure Agents (Workers)
Agents are the help desk staff who work on tickets.

- Click Admin Panel → Agents → Agents
- Click "Add New Agent"
- Create first agent:
  - First Name: Jane
  - Last Name: Doe
  - Email Address: jane.doe@helpdesk.com
  - Username: jane.doe
  - Click "Set Password" and create password
  - Uncheck "Send the agent a password reset email"
  - Under Access tab:
    - Primary Department: System Administrators
    - Role: Supreme Admin
    - Extended Access: Support Department (Support role)
  - Under Teams tab:
    - Assign to Level II Support team
  - Click "Create"

- Create second agent:
  - First Name: John
  - Last Name: Doe  
  - Email Address: john.doe@helpdesk.com
  - Username: john.doe
  - Set password and configure similar to Jane
  - Primary Department: Support
  - Role: View only
  - Teams: Level I Support
  - Click "Create"

### Step 7: Configure Users (Customers)
Users are the customers who submit tickets.

- Click Agent Panel (toggle from Admin Panel)
- Click Users → User Directory
- Click "Add New"
- Create first user:
  - Email Address: karen@osticket.com
  - Full Name: Karen Karen
  - Phone Number: 555-555-5555
  - Click "Add User"

- Create second user:
  - Email Address: ken@osticket.com
  - Full Name: Ken Ken
  - Phone Number: 555-555-5551
  - Click "Add User"

### Step 8: Configure SLA Plans
SLA (Service Level Agreement) plans define response and resolution times.

- Click Admin Panel → Manage → SLA Plans
- Click "Add New SLA Plan"
- Create "SEV-A" (Severe):
  - Name: SEV-A
  - Grace Period: 1 hour
  - Schedule: 24/7
  - Click "Add Plan"

- Create "SEV-B" (High):
  - Name: SEV-B
  - Grace Period: 4 hours
  - Schedule: 24/7
  - Click "Add Plan"

- Create "SEV-C" (Normal):
  - Name: SEV-C
  - Grace Period: 8 hours
  - Schedule: Monday - Friday 8am-5pm with U.S. Holidays
  - Click "Add Plan"

### Step 9: Configure Help Topics
Help Topics categorize tickets and can trigger specific workflows.

- Click Admin Panel → Manage → Help Topics
- Note default topics exist (General Inquiry, Feedback, Report a Problem)
- Click "Add New Help Topic"
- Create "Business Critical Outage":
  - Topic: Business Critical Outage
  - Status: Active
  - Type: Public
  - Parent Topic: (leave blank for top-level)
  - SLA Plan: SEV-A
  - Auto-assign to: System Administrators
  - Click "Add Topic"

- Create "Equipment Request":
  - Topic: Equipment Request
  - Status: Active
  - Type: Public
  - SLA Plan: SEV-B
  - Auto-assign to: System Administrators
  - Click "Add Topic"

- Create "Password Reset":
  - Topic: Password Reset
  - Status: Active
  - Type: Public  
  - SLA Plan: SEV-B
  - Auto-assign to: Support
  - Click "Add Topic"

- Create "Personal Computer Issues":
  - Topic: Personal Computer Issues
  - Status: Active
  - Type: Public
  - SLA Plan: SEV-C
  - Auto-assign to: Support
  - Click "Add Topic"

### Step 10: Test the Configuration
- Navigate to the end-user portal: http://localhost/osTicket/
- Click "Open a New Ticket"
- Verify that:
  - Help Topics appear in dropdown
  - You can create a ticket without logging in
  - Ticket is assigned to correct department based on Help Topic

### Step 11: Test Agent Access
- Log out of admin panel
- Navigate to: http://localhost/osTicket/scp/
- Log in as one of the agents you created (jane.doe)
- Verify agent can see tickets assigned to their department
- Test creating internal notes and responses

### Step 12: Verify Email Settings (Optional)
If email is configured:
- Create a test ticket
- Verify confirmation email is sent to user
- Verify agent notification email is sent
- Test email responses (if configured)

## Configuration Complete!

Your osTicket system is now configured with:
- Proper role-based access control
- Multiple departments and teams for ticket routing
- SLA plans for response time management  
- Categorized help topics for better organization
- Agent and user accounts for testing

The system is ready for production use and can handle tickets with appropriate prioritization and routing based on your organizational needs.
