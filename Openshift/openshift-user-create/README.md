## Create Openshift user 

1. Create a User `abc`   
```Bash
$ oc create user abc
  user.user.openshift.io/abc created
```
2. Get user `abc`   
```Bash
$ oc get user abc
NAME    UID                                    FULL NAME   IDENTITIES
abc   xxxxx...................... 
```   
3. Create password for user `abc` using htpasswd 
```Bash
$  htpasswd -c -b abcpasswordfile abc abc1234
  Adding password for user abc
```   
4. cat abcpasswordfile file which contain user `abc` password.
```Bash
$ cat abcpasswordfile 
abc:$apr1$NV.vn5CS$ABCDEFGHIGKH
```   
5. Add `edit` role to user `abc`
```Bash
$ oc adm policy add-role-to-user edit abc
clusterrole.rbac.authorization.k8s.io/edit added: "abc"
```  
6. Get rolebinding for user `abc`   
```Bash
$ oc get rolebinding
NAME                               ROLE                                           AGE
edit                               ClusterRole/edit                               10m
```   
7. Create secret in openshift-config namespace which contain user `abc` password
```Bash
$ oc create secret generic htpass-secret-abc --from-file=htpasswd=abcpasswordfile -n openshift-config
  secret/abcpasswordfile created
```
8. Edit oauth resource and add new HTPasswd at the end of oauth resource  
```Bash
oc edit oauth cluster
```
add new HTPasswd at the end of oauth resource  
```bash
  - htpasswd:
      fileData:
        name: htpass-secret-abc
    mappingMethod: claim
    name: htpass-secret-abc
    type: HTPasswd 
``` 
save changes and exit 
```Bash
 oauth.config.openshift.io/cluster edited
 ```
9. Create identity 
```Bash
$ oc create identity htpass-secret-abc:abc
  identity.user.openshift.io/htpass-secret-abc:abc created
```  
10. Get identity
```Bash
$ oc get identity htpass-secret-abc:abc 
NAME                    IDP NAME                 IDP USER NAME   USER NAME   USER UID
htpass-secret-abc:abc   htpass-secret-abc        abc             abc        xxxxx......................
```
11. Create useridentitymapping
````Bash
$ oc create useridentitymapping htpass-secret-abc:abc abc
  useridentitymapping.user.openshift.io/htpass-secret-abc:abc created
````
9. Logout current user and then login with user `abc`  
````Bash
 oc logout
Logged "xyz" out on "https://"
````
10. logint abc 
```Bash
oc login -u abc -p abc1234
Login successful.

You don't have any projects. You can try to create a new project, by running

    oc new-project <projectname>
```