## Build and Validate an Automated Backup System with Azure Blob Storage, Terraform, and Logic Apps

### Objective

This SOP explains how to create an automated backup solution using Azure Blob Storage with versioning and lifecycle management, Terraform for infrastructure deployment, and Logic Apps for daily confirmation emails. It also covers validation steps to confirm that backups, versioning, and alerting are working correctly.

### Link to Loom

<https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0>

### Key Steps

**1. Define the backup system components and required variables** [0:00](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=0)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5a8742c2-a5cd-4001-905d-a3660cfdd3ce" />


- Confirm the solution will include: 
  - Azure Blob Storage with versioning enabled
  - Lifecycle management policies to move older data to cheaper tiers
  - A Logic Apps workflow to send daily backup confirmation emails
- Identify the core variables needed for deployment: 
  - Location/region
  - Resource name(s)
  - Alert email address
  - Tags
- Verify the deployment region is correct before proceeding, especially if using a student or restricted Azure subscription.

 

**2. Prepare the Terraform configuration structure** [0:20](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=20)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/99da5364-9f6d-4d2a-b209-a1f7c1e343e6" />


- Create or review the Terraform codebase that will deploy the backup environment.
- Ensure the configuration includes: 
  - Provider setup
  - Terraform initialization settings
  - Variable definitions
  - Output values for key resources and email-related settings
- Confirm the variables are mapped correctly so the alert email and other values are passed into the deployment.

 

**3. Configure deployment variables and outputs** [0:39](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=39)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f385f5b3-d580-4b63-9f30-c571abbfe54e" />


- Populate the variables with the correct values: 
  - Location
  - Name
  - Alert email destination
  - Tags
- Verify outputs are configured so important deployment details can be referenced later.
- Double-check that the email output points to the intended recipient address.

 

**4. Create the Azure resource group and storage resources** [1:08](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=68)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5b476fe4-746b-40ea-be31-51ebeb074765" />


- Define and deploy the Azure resource group.
- Create the storage account that will hold backup data.
- Add the storage container associated with the storage account.
- Confirm the storage account is created before the container and that the resources are linked correctly.

 

**5. Add access roles, backup policies, and storage management settings** [1:36](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=96)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9fac9b60-8a5e-426f-80a8-bd9bf5c9ecd4" />


- Configure the roles required for the storage account and backup workflow.
- Apply the storage policies that support backup retention and lifecycle behavior.
- Enable versioning so multiple versions of the same file can be retained.
- Set lifecycle management rules to move older data to lower-cost storage tiers as needed.

 

**6. Deploy monitoring and logging resources** [1:58](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=118)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/349d08fd-b75c-43b5-8d52-c9a60108bf2a" />


- Create a Log Analytics Workspace for monitoring and diagnostics.
- Configure the following settings: 
  - Resource group
  - Workspace name
  - Location
  - Tags
  - SKU
  - Diagnostic settings
- Ensure diagnostic data is routed correctly for visibility into the backup system.

 

**7. Set up alerting and notification components** [2:14](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=134)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3aad3e82-5361-478c-825e-1a7dc5b4d5e1" />


- Create a Monitor Action Group for backup notifications.
- Add the email receiver using the designated alert email address.
- Create a Monitor Metric Alert that triggers when the defined metric threshold is reached.
- Confirm the alert is connected to the action group so notifications are sent automatically.

 

**8. Build the Logic App workflow for daily backup confirmation** [2:22](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=142)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/abf9a8e4-4348-49f7-8f5b-4066ff86e7d4" />


- Create a Logic App Workflow dedicated to backup confirmation emails.
- Configure the workflow to run daily at the required time.
- Set the workflow to reference the storage account and the documents folder location.
- Add the email action that sends a daily backup confirmation message.
- Define the email subject and body so the message clearly communicates backup status.

 

**9. Format the confirmation email content** [3:46](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=226)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bf797863-4155-4b6e-aaaa-75864b02d319" />


- Set the email subject to something clear, such as: 
  - Daily Backup Confirmation
  - Backup System Status
- Write the email body to include the backup status and any relevant details.
- Apply formatting options as needed for: 
  - Date
  - Time
  - Body length or layout
- Make sure the email is easy to read and clearly indicates whether the backup process is functioning.

 

**10. Test the Logic App email delivery** [4:07](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=247)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/64f80fb3-271a-4ffc-93cc-aa4824eeb251" />


- Send a test email from the Logic App workflow.
- Confirm the message arrives in the intended inbox.
- Verify the email content displays the expected backup status information.
- If the email does not arrive, check the workflow trigger, email connector, and recipient address.

 

**11. Validate blob versioning with test files** [4:55](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=295)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/44a05fe2-d4a5-49c1-9936-1568f89ffad6" />


- Upload a test file to the storage container.
- Create a second version of the same file to confirm versioning is enabled.
- Verify both versions are retained in storage.
- Use the appropriate command or storage view to confirm the versions exist as expected.

 

**12. Confirm the automated backup system is working end to end** [5:29](https://loom.com/share/db11a6bfe83b464ea023ac1dd0229fb0?t=329)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/47223859-8b0d-47f4-bb35-d6c10a249b1d" />


- Review the final output to ensure: 
  - Storage resources were created successfully
  - Versioning is active
  - Lifecycle and backup policies are in place
  - Daily confirmation emails are being sent
- Validate that the backup workflow behaves as intended when files are updated.
- Document any issues encountered and the steps taken to resolve them for future reference.

### Cautionary Notes

- Ensure the Azure region is correct before deployment, especially in restricted or student subscriptions.
- Confirm the alert email address is accurate to avoid missed notifications.
- Verify resource creation order in Terraform so dependent resources are created after their prerequisites.
- Test both email delivery and file versioning; a successful deployment alone does not guarantee the backup workflow is functioning.
- If lifecycle policies are misconfigured, data may move to cheaper tiers earlier or later than intended.

### Tips for Efficiency

- Use Terraform variables and outputs consistently to reduce manual edits.
- Keep resource names, tags, and email settings centralized in one variables file.
- Test the Logic App with a sample email before relying on it for production notifications.
- Upload a small test file first when validating versioning to avoid unnecessary storage usage.
- Reuse the same validation checklist after any future changes to the backup workflow.
