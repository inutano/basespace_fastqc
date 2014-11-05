Scripts inside the docker container illumina/fastqc for basespace native app
===============

just copied scripts from /home/apps/fastqc of the [docker container published as illumina/basespace on docker hub](https://registry.hub.docker.com/u/basespace/fastqc/).

### Directory

```
fastqc
|- download
|- output
|- fastqc.py
|- lib
  |- __init__.py
  |- __init__.pyc
  |- docker_app.py
  |- docker_app.pyc
  |- parse_into_tables.py
  |- parse_into_tables.pyc
  |- simple_fastqc.py
```

### Form Builder

form

```
{
    "$type": "Form",
    "fields": [
        {
            "$type": "TextBox",
            "size": 300,
        	"value": "default value!",
        	"label": "App Session Name",
        	"required": true,
        	"requiredMessage": "Please enter name for your app session.",
        	"id": "app-session-name",
        	"helpText": "this help text will display next to the control in a pop over, damnass!"
        },
        {
            "$type": "SampleChooser",  
            "size": 300, 
            "allowedPermissions": "read", 
            "label": "Input Sample",
            "required": true,
            "requiredMessage": "Please choose a sample",
            "id": "sample-id"           
        },
        {
            "$type": "SectionBreak"
        },
        {
            "$type": "ProjectChooser",
            "size": 300,
            "valueType": "Output",
            "allowedPermissions": "owner",
            "label": "Output Project",
            "required": true,
            "requiredMessage": "Please choose a project",
            "id": "project-id"
        },
        {
            "$type": "SectionBreak"
        }
    ],
    "rulesets": [],
    "id": "form-container"
}
```

callback.js

```
function launchSpec(dataProvider){
    var projectId = dataProvider.GetProperty("Input.project-id").Id;
    var retval = { 
       commandLine: ["python", "/home/apps/fastqc/fastqc.py", projectId],
        containerImageId: "basespace/fastqc"
    
    };
    return retval;     
}
```

