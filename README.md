# OmniPlan OmniFocus Task Sync

[https://github.com/richm8080/OmniPlanFocusSync](https://github.com/richm8080/OmniPlanFocusSync)

## 1. Introduction

These scripts enable tasks to be sent from OmniPlan to OmniFocus and subsequently kept in sync.

The scripts utilise the OmniAutomation API provided in the PRO versions of OmniPlan 4 and OmniFocus 3.

## 2. Credits

The scripts are inspired by (but completely unrelated to) both:

* the AppleScripts provided by Felix Chenier [here](http://felixchenier.com/focusplan); and
* the scripts provided on the Omni Automation website [here](https://omni-automation.com/omniplan/app-to-app.html)

These scripts do not work in the same way as the above however - several modifications have been made. See below for how these scripts work.

## 3. DISCLAIMER

These scripts work for me but they may not be suitable for you. I strongly suggest that you review the code, and test functionality thoroughly before using the scripts on anything live.

**I am not, nor will I be held responsible for any corruption or other loss of data resulting from the use of these scripts. Use them at your own risk**

## 4. How to use

The pro versions of both OmniFocus 3 and OmniPlan 4 are required.

Save the scripts to your OmniPlan 4 Plug-Ins directory.

The scripts will provide 4 new menu options on the Automation menu.

* Copy All Tasks To OmniFocus
* Copy Selected Tasks To OmniFocus
* Pull Updates From OmniFocus
* Push Updates To OmniFocus

### 4.1 Copy All Tasks To OmniFocus / Copy Selected Tasks To OmniFocus

These options will loop through either all, or the selected tasks, from the open OmniPlan document.

Items meeting the following criteria will be copied into the inbox in OmniFocus:

* Task is incomplete (<100%)
* Task doesn't already have an assigned OmniFocusID
* Task type is 'task' (i.e. not a group, milestone or hammock task)

Everything else will be ignored.

The project hierarchy will **not** be mirrored in OmniFocus.

The data fields copied are as follows:

| OmniPlan | OmniFocus | Notes |
| ------------- | ------------- | ------------- |
| Project Name | Tag | A tag will be created with the project name under a parent tag 'OmniPlan', these will be created if they do not already exist. |
| Task Name | Task Title | |
| Task Note | Task Note | A hyperlink will be appended to the note field in both OmniFocus and OmniPlan allowing you to click through to see the corresponding item in the other application. |
| Task End Date | Task Due Date | This copies over with the precise date and time as set in OmniPlan as the due date and time in OmniFocus |
| Task Start No Earlier Than Date | Task Defer Date | The defer date and time will only be set if there is a 'Start No Earlier Than' constraint on the task |

On successful completion, OmniFocus will then return the OmniFocusIDs for each of the tasks to OmniPlan where this field will be created if it doesn't already exist and each task transferred will have its OmniFocusID set.

The note in OmniPlan will also have a hyperlink appended to enable click through to the task in OmniFocus.

### 4.2 Pull Updates From OmniFocus

This option will send a list of tasks from OmniPlan to OmniFocus where there is an OmniFocusID set on the task in OmniPlan.

OmniFocus will loop through the list of OmniFocusIDs, where the ID is valid, it will return the completion status of the task in OmniFocus which in turn will set in OmniPlan.

---

CAUTION! OmniFocus stores completion as a boolean variable therefore any granularity of completion will be lost:

* If the task is **incomplete** in OF the completion will be set to **0%** in OP.
* If the task is **complete** in OF the completion will be set to **100%** in OP.

---

#### Other Points To Note:

Where the OmniFocusID is invalid (e.g. if the task has been deleted from OF) then the OmniFocusID will be cleared in OmniPlan. Note that the task note field will NOT be amended, the URL link will remain in place even though it has become invalid.

Task dropped status is not observed by the script so dropping a task in OmniFocus will not have any effect on the task in OmniPlan.

### 4.3 Push Updates To OmniFocus

This option will send a list of tasks from OmniPlan to OmniFocus where there is an OmniFocusID set on the task in OmniPlan.

OmniFocus will loop through the list of OmniFocusIDs, where the ID is valid, it will update the task. The following fields will be updated (in OF):

* Task Title
* Task Due Date
* Task Defer Date
* Task Completion

(see table in 4.1 for details of what will be set on these fields)

## 5. Contributions
This is my first foray into OmniAutomation scripts, and indeed my first time making any of my code public.

These scripts work for me but they may not be suitable for you, I am also aware that there is a lot of repetition between the components and something could be improved by utilising a library plugin.

Contributions are welcome, if you have any improvements to suggest feel free to submit a pull request.
