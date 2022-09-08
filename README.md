# Salesforce-Tricks
Just some tips and tricks I encountered working on salesforce as a platform 

## Download Debug Logs in Bulk
Here's how you can download multiple debug logs at once using sfdx cli: 
```bash
sfdx force:apex:log:list | sed '1,2d' | sed 's/^[[:alpha:]]*[[:space:]]*[[:digit:]]*[[:space:]]*//g' | sed 's/[[:space:]].*//g' | while read line; do sfdx force:apex:log:get --logid $line > path_to_log_folder/$line ; done
```

additionally you can add a `head -n count`  if you wanna restrict the number of logs you wanna download

eg. downloading first 15 logs
 ```bash
sfdx force:apex:log:list | head -n 15 | sed '1,2d' | sed 's/^[[:alpha:]]*[[:space:]]*[[:digit:]]*[[:space:]]*//g' | sed 's/[[:space:]].*//g' | while read line; do sfdx force:apex:log:get --logid $line > path_to_log_folder/$line ; done
```

you can also filter these by specific users by adding the following filter `grep -i 'user name'` 

eg. download all logs from user John Doe 
 ```bash
sfdx force:apex:log:list | grep -i 'John Doe' | sed '1,2d' | sed 's/^[[:alpha:]]*[[:space:]]*[[:digit:]]*[[:space:]]*//g' | sed 's/[[:space:]].*//g' | while read line; do sfdx force:apex:log:get --logid $line > path_to_log_folder/$line ; done
```
