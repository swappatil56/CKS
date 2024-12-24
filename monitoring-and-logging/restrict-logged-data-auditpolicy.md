## We want to restrict logged data with an Audit policy-


1. Nothing from stage requestreceived
2. Nothing from get watch list
3. Secret only metadata level
4. everything else requestresponse level

steps- 

1. change policy files
2. disable audit logging in api server
3. enable autit logging in api
   - if api doesn't come up check for error logs in /var/log/pods/kube-system_kube-api*
   - test your changes

4. test your changes