# 📜 Roles & Capabilities  
### Role Updates & Deployment  
- Add a note about the rake task for role updates and how deployment updates roles.  
- Global roles should only show one role: **Tenant Admin**, **Supervisor**, or **Learner**.  

### Capabilities  
- `canShareSharedContent` & `canUpdateSharedContentEnrolmentLimits` (tenant settings).  
- Ensure group-level roles only apply to group content and group users.  

---

# ⚙️ Tenant Settings  
### Configuration  
- Tenant settings for certificates.  
- Make tenant URL optional.  
- Set `shortname` mandatory and sanitise it for URL-friendly strings.  
- Create `TenantFeatureSettings` type and set default values for enabled features upon creation.  
- Ensure frontend and backend default settings match.  

### Data Update  
- Write a Rails script to update all existing tenant settings.  

---

# 🛠️ UI & UX Improvements  
### General Improvements  
- Add breadcrumbs.  
- Create audit log tables in the database to track user actions.  
- Ensure the navigation sidebar in slim mode shows labels on hover.  
- Add a right-hand settings panel for **Pathways**.  
- Fix slight jump in the actions menu in tables.  
- Ensure modals on table pages are consistent.  

---

# 📧 Notifications & Email  
### Notifications  
- Use the `Noticed` gem for handling notifications (emails & general notifications).  
- Ensure SCORM upload notifications appear on top.  

### Email Enhancements  
- Add confirmation when deleting a tenant.  
- Check email images for tenants with SVG logos.  
- Allow changing email addresses for existing users.  

---

# 🏗️ Course Builder Enhancements  
### Layout & Design Options  
- Add new layout options:  
  - **Numbered list**  
  - **Checkbox list**  
  - **Statement blocks with various styles**  

### Additional Features  
- Expand the course builder with:  
  - **Flip cards**  
  - **Cover page options**  
  - **Lesson header options**  
  - **Collaboration features**  
  - **Full-screen view for course modules**  

### File Handling  
- Verify Storyline files import correctly.  
- Push "View Course" to full screen.  

---

# 🐛 Bug Tracking & Fixes  
### Known Issues & Fixes  
- Fix: Deleting groups does not update the groups column in the users table.  
- Fix: Cannot update `BulkActionsMenu` while rendering `TableProvider`.  
- Fix: Date on certificates not displaying correctly.  
- Fix: Search not working in categories.  
- Fix: Audio not showing when added to a course.  

### User Deletion  
- Thoroughly test deleting users—ensure dependent models still work.  

---

# 📦 Reseller & Training Company Use Cases  
### Reseller  
- Can sell our catalogue to organisations without LMS functionality.  

### Training Company  
- LMS-only or with our catalogue.  
- Can create their own courses.  

---

# 🏢 Organisation Management  
### Organisation Leaders  
- Upload new users to the same organisation.  
- Assign group-provisioned courses to users.  
- See reports.  
- Add capability to assign content at the group or tenant level.

---

[Visit For More Details](https://sunand-e.github.io/Zanda-wiki/Overflow-List)