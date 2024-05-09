# Approval-Flow
## Project Overview
Xyz Limited is a company that has series of processes, which requires the review and the approval of the supervisors and the management for certain processes to be approved.The current process carried out, Employee A, Creates a spreedsheet, with request for budget, which contains details like the items, the reason for the leave, the total amount breakdown. Employee A spends days preparing that budget, that budget created is now then sent to a supervisor, The supervisor downloads the file, reviews it, and if they are comment he sends that comment back to the employee for Employee A to resolve.If they are no issue, the Supervisor hence then sends it to the Finance Team.This significantly leads to long time for approvals of various processes, and also no unified database to maintain what has been shared. he goal of this project is to significantly reduce the amount of time needed for the approvals of various process like Budget/Leave.
### Mapping the Company's Curent Assets
Current Tools used by XYZ company limited
1. Excel
2. Word

License Available
Office365 E5 Apps for Enterprise.

### Solution Recommendation
From a detailed study on XYZ business requirement and current process, I have been able to device a solution which would significantly;
1. Create a sharepoint list where users would be able to Select the type of process request they require
2. Build out Approval Flow which alerts the manager and the finance team anytime a new item/request has been made. Also the user has the ability to upload series of attachment which the management team would be able to go into inside the body of the Approval mail.


### Tools Used for Project
1. Sharepoint 
2. Powerautomate


### Solution Build
#### Sharepoint List Build
Creating the Sharepoint list, if you don't already have a sharepoint site, You have to create a sharepoint, to easily do that navigate to office.com, Click on apps, then proceed to click on sharepoint. At the top section you would the option to create a site. Once you have created the site, You need to create the list, By clicking on the new button. Your list should include, the following columns;
1. Items (Text Data Type)
2. Request Date (Date Data type)
3. Amount (This can be a currency field)
4. Category (A choice list which contains options which the user can select what his/her request falls under).
5. Description (This can be a Multi-line text)
6. Attachments
7. Approval Status
8. Approval Info.
9. Created By (This is created by default).

You can set a custom view and set that as the default, for a better experience.

#### Flow Build
Kindly find below the flow Chart and detailed explanation of each section

1. Trigger- Automated Cloud flow, When an item is modified in sharepoint trigger selected
2. Trigger Condition- Because we are going to need the flow to run on everytime someone modifies the list, we need to specify a condition that triggers the flow, to avoid the flow from becoming an endless loop running. Two Conditions set - 
- @or(equals(triggerBody()?['ApprovalStatus']?['Value'],'New') Checks if the approval status is New,
equals(triggerBody()?['ApprovalStatus']?['Value'],'Rejected') Checks if the approval status is rejected),
Hence this are the two reasons why the flow should be triggered, Someone must either submit a new request or edit a rejected request.
3. Stop sharing an Item or a file action (When someone creates an approval, the person shouldn't interupt the process and thus cause an endless loop, this ensures once the employee has made the request, the approval goes on forward, but the employee wouldn't edit or update until the request has been accepted or rejected, for this to be done effectively, a configuration was done on sharepoint, by clicking on the list setting and navigating to permission for the list).
4. Update Item: Inside this section we would update the items of all the columns with the dynamic contents from the trigger.
5. Grant access to a folder action (In this section we would specifically be using this action to grant access to a specific user (the author) and the access would be to view.
6. Initialize Variable (This is used to create a variable array for the attachment)
7. Get attachments from sharepoint action in Powerautomate
8. Apply to each action which contains (Get attachment content and append to array variable loop) this is used to attach the attachments into an array if they are more than one attachment
9. Start and Wait for an Approval action (Everyone must approve the flow, and input the required people in the assigned to column)
10. Create an HTML Table action (This table helps us update the approval info so the user can see what each approver selected, and the response time).
11. Condition action, (This checks if the status is approved or rejected, If it's approved it should update the necessary fields, if it's rejected, it should update the approval status to rejected and the user should be granted permission to edit the list and resubmit the flow again.
