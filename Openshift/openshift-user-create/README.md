## Create Openshift user 

1. Create a User
```Bash
$ oc create user user8
  user.user.openshift.io/user8 created
```
1. Get user
```Bash
$ oc get user user8
NAME    UID                                    FULL NAME   IDENTITIES
user8   50d4a40e-3127-46bf-b3c9-663d7e97b956 
```   
1. Create password using htpasswd 
```Bash
$  htpasswd -c -b user8passwordfile user8 openshift
  Adding password for user user8
``` 
1. Add edit role to user 
```Bash
$ oc adm policy add-role-to-user edit user8
clusterrole.rbac.authorization.k8s.io/edit added: "user8"
``` 
1. Create secret in openshift-config namespace which contain user8 and user8 password
```Bash
$ oc create secret generic htpass-secret-user8 --from-file=htpasswd=user8passwordfile -n openshift-config
  secret/htpass-secret-user8 created
```
1. Edit oauth resource and add new HTPasswd at the end of oauth resource  
```Bash
oc edit oauth cluster
```
add new HTPasswd at the end of oauth resource  
```bash
  - htpasswd:
      fileData:
        name: htpass-secret-user8
    mappingMethod: claim
    name: htpass-secret-user8
    type: HTPasswd 
``` 
save changes and exit 
```Bash
 oauth.config.openshift.io/cluster edited
 ```
1. Create identity 
```Bash
$ oc create identity htpass-secret-user8:user8
  identity.user.openshift.io/htpass-secret-user8:user8 created
```
1. Create useridentitymapping
````Bash
$ oc create useridentitymapping htpass-secret-user8:user8 user8
  useridentitymapping.user.openshift.io/htpass-secret-user8:user8 created
````
1. Logout current user example logout maaz  
````Bash
 oc logout
Logged "maaz" out on "https://"
````
1. logint user8 
```Bash
oc login -u user8 -p openshift
Login successful.

You don't have any projects. You can try to create a new project, by running

    oc new-project <projectname>
```