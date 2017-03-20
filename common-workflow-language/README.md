## Install cwl tool

* Refer to this link: [https://github.com/common-workflow-language/cwltool](https://github.com/common-workflow-language/cwltool)

* Install

```
pip install cwlref-runner
```

## A 'Hello world' example

* Step 1: create two files: one **.cwl** to describe what tools to use, and to specify inputs and outputs; the other file is
      **json** or **yml** to describe the input argument-value mappings.
      
    + *1st-tool.cwl*
      
     ```
     cwlVersion: v1.0
     class: CommandLineTool
     baseCommand: echo
     inputs:
       message:
         type: string
         inputBinding:
                position: 1
     outputs: []
     ```
     
    + *echo-job.yml*
     
     ```
     message: Hello world!
     ```
* Step 2: Run the workflow with **cwl tool**

    ```
    cwl-runner 1st-tool.cwl echo-job.yml
    ```

