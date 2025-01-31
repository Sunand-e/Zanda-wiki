### This is an unordered overflow list - some of these are bugs, some are notes, some are finished tasks.

Roles/capabilities - ADD NOTE ABOUT RAKE TASK and how deployment updates the roles

Tags / categories

tenant settings for certificates
- Logo
- 'Awarding body logo' in bottom left
- 'Awarding body text' underneath


When deploying, github needs an IAM role, with policies attached which will 
allow for registration of a task definition, and allow for deploying images
to AWS's Elastic Container Registry (ECR). Currently this role is called `ExampleGithubRole`

canShareSharedContent & canUpdateSharedContentEnrolmentLimits tenant settings


- Notifications (Emails, general notifications - look at Noticed gem)

Create a tag type - competence
######################

 - Notification for scorm upload should not appear behind
 
 - Make tenant url optional and 'shortname' mandatory, and sanitise for URL-friendly strings
 - ???? check: "Should not send shortname with tenant creation request from woocommerce plugin (??)

 - 'Global roles' should only show one role - tenant admin, supervisor or learner.

 - Breadcrumbs 
 - Audit log tables in db so we can see who did what, and when
 - Use ActiveRecord's counter cache / counter_culture gem to optimise fetching the size of a record's association 

 - Slight jump in actions menu in tables

 - deleting groups does not update the groups column in the users table 
 
 - additionalParams?.group_id should be refactored out of uploadFilesAndNotify. This is used when doing a bulk user import

- Move from using Apollo's 'onCompleted' to using async/await

 - Make it easier to do bulk assignments/provisioning/sharing of content for users/groups/tenants:
   - an expandable tree-structure using categories, with accordian-style
   

 
Things to check:
 - check update of 'groupsAssigned' field of content when assigning content to groups
 @@@@ no optimistic update for 'assignedGroups' field of content item. Not required until
 we need to show/update a list of groups which have been assigned the content
 - audio not showing when added??
 - Pathways - needs a right hand settings panel
 - Nav sidebar in slim mode needs labels on hover
 Have to refresh to see courses in reports
 - invalidate reports when users added to or removed from groups/content
CHECK REPORTING GROUP FILTER TABLE VALUES
 - not showing correct values upon load, but is corrected after visiting the group edit page
Thorough test of deleting users - do all dependent models still work
 - check reports 
 
 ###########################################

- Groups / organisations visibility in menu

- Add new user (group leader) - if user can add new users in a group context, and the user has mult must specify which group to add to.
	- if not specified, error should be returned
	
- filters for groups in user list

- order of user in user list

- user group role bug in users page



Fix 
Warning: Cannot update a component (`BulkActionsMenu`) while rendering a different component 
(`TableProvider`).


nEED TO SEARCH USERS ON EMAIL ADDRESS


Only allow tenant admins to change others' email addresses
WHEN SUPER ADMIN BELONGS TO AN ORGANISATION, CANT DELETE USERS??
Can't delete scorm packages from encirc360??
Category didn't copy across when sharing course from elearningplus to encirc
Creating a new section in course builder - not reflecting in UI until refresh - (check lessons also)

course builder
A numbered list and checkbox list
Need a paragraph with heading option
Text and button option
More divider options
Ability to create a theme
Labelled graphic / Hotspots
Need a paragraph with subheading option
Statement block with various style options
Flip cards
Cover page options
Lesson header options
Import Storyline files
Knowledge check options
Quote block with various style options
Statement block with various style options
Collaboration on course builder
Push view course to full screen
Add page title tags
Verify Login flow is self-explanatory - check mobile too
Check email images for tenants with svg logos
Allow changing email addresses for existing users
Add a confirmation when deleting a tenant
Fix font dropdowns in tenant settings
Fix: search not working in categories
Check (& fix?): remove course image not working
Fix: date on certificates
Fix: certificate table text on top of certificate modal
Check (& fix?): all modals on table pages?
Add a 'goFullScreen' to course modules


Set default values for tenant settings 'enabled' features upon creation
Create `TenantFeatureSettings` type

ensure upon tenant creation, all features' 'enabled' values are set
search for .enabled, replace relevant occurences with useTenantFeaturesEnabled	
search for requireEnabledFeatures, update to use useTenantFeaturesEnabled



Ensure frontend & backend default settings are the same


write a rails script to update all existing tenant settings




####################
Reseller - can sell our catalogue to Organisations

Training Company - like a reseller, but can use course builder

End user company
 - Has own tenant, with groups or
 - is an organisation under elp tenant
 
 
 
########################################
Course Catalogue and LMS Use Cases (Oct 2024)
########################################

Us – Catalogue only – directly to clients (ORGANISATIONS on Courses.Zanda360.com)
Us – Catalogue only – via eCommerce to organisations (ORGANISATIONS on Courses.Zanda360.com?) – assume this needs a change to the eCommerce Store?????

Us – LMS Only
Us – LMS plus Catalogue - tiered subscription pricing OR Base Price & Credits

Reseller – Catalogue – No LMS functionality (ORGANISATIONS on Reseller Tenancy)

Training company – no catalogue, their own courses - LMS Only
Training company – Our Catalogue (as a Reseller) plus their own courses.
     - (GROUPS and ORGANISATIONS on Training Company Tenancy?)
	 
Training company – Zanda credits & training company credits
########################################
Organisation Leader
 - Upload new users TO THE SAME ORGANISATION (group)
 - Assign groupProvisionedCourses to users within the organisation
 - See reports

Only people with 'GetGroupProvisionedCourses' can get group provisioned courses
 - create new capability, add to:
   - tenant admin
   - supervisor
   - group leader
 - ensure capabilities of group roles only apply to the group, e.g. group content & group users
 
 - upload users capability is applied at group level for Group Leader. Need to either:
  - 

 - GetGroupProvisionedCourses 
 
 
 
 
 
 Group Leader   - enrolusersincontent
 
 for each user in the user's list, a new action - assign courses ( /pathways / resources )
 
 if global 'enrolusersincontent', the content available for assigning should be the same as all 
 courses assigned to the current user.
 
 otherwise(?),
 
 if the user belongs to any group which the current user has 'enrolusersincontent' capability in,
 the content available for assigning should be the group's "available courses".
 
 Scenario:
 current user has been assigned Course A, and has global 'enrolusersincontent' capability.
 
 if user can enrolusersincontent at tenant level,
	can assign to a user any content which the current user has been assigned
	
if user can enrolusersincontent at a group level,
	can assign to a user any content which has been provisioned to the group

#########################################