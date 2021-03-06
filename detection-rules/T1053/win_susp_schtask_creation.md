# Testing Documentation win_susp_schtask_creation

## Detection Rule
```
title: Scheduled Task Creation
status: experimental
description: Detects the creation of scheduled tasks in user session
author: Florian Roth
logsource:
    category: process_creation
    product: windows
detection:
    selection:
        Image: '*\schtasks.exe'
        CommandLine: '* /create *'
    filter:
        User: NT AUTHORITY\SYSTEM
    condition: selection and not filter
fields:
    - CommandLine
    - ParentCommandLine
tags:
    - attack.execution
    - attack.persistence
    - attack.privilege_escalation
    - attack.t1053
    - attack.s0111
falsepositives:
    - Administrative activity
    - Software installation
level: low
```

## Attack Simulation
Create a Scheduled Task with cmd.exe:
```
SchTasks /Create /SC Daily /TN "My Task" /TR "C:Test.bat"
```

## Result

Splunk

![](https://github.com/P4T12ICK/Sigma-Rule-Repository/blob/master/detection-rules/T1053/win_susp_schtask_creation_test.png)

## Note
- Detection rule tested successfully.



