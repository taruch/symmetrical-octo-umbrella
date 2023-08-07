This repo enables you to add ServiceNow ITSM templates to your Ansible Automation Platform Controller.  The point of them is to make it\
easy to showcase adding ITSM capabilities to your workflows.

Prereqs in your AAP Controller to run the servicenow_templates_create playbook:
- "localhost" inventory 
- "ServiceNow Demo Example" project

To add the ServiceNow Templates to your Ansible Automation Platform Controller, set up the project in AAP Controller.\
Project Name: ServiceNow Demo Examples\
Project Organization: Default\
Project Source Control Type: Git\
Project Source Control URL: https://gitlab.com/redhatautomation/aap_servicenow_demos.git

Then, you can either create a ServiceNow Setup Template using the ServiceNow Demo Examples project and the servicenow_templates_create.yml template, or run the following using Ansible Navigator:\
ansible-navigator run -mstdout servicenow_templates_create.yml -e "user=CONTROLLER_USER" -e "pass=PASSWORD" -e "controller=ANSIBLE_CONTROLLER_HOST_HERE"


Creates the following templates in your controller:
- ITSM Create Change Ticket
- ITSM Update Change Ticket
- ITSM Close Change Ticket
- ITSM Create Incident Ticket
- ITSM Add CMDB CI
- ITSM List CMDB CI

The "ITSM Create Change Ticket" will create a change ticket and forward the change ticket number to the next step in a workflow.\
\
The "ITSM Update Change Ticket" template requires a change workflow in ServiceNow that doesn't require CAB approval.  If you don't
have this then it will only move the ticket through the "scheduled" stage.\
\
The "ITSM List CMDB CI" is written to where it will either grab all of the CI's, or it will do a query, but defaults to neither.
- Grabbing all of the CI's takes a very long time (YMMV dependant on how many CIs are in your database), so beware about using this option.
To use this option, add a tag of 'all' to your template.
- Doing a query requires you to add a variable (either through a survey or just adding a default variable to the template) of SYS_CLASS_NAME. 
To use this option, add a tag of 'limited' to your template.


