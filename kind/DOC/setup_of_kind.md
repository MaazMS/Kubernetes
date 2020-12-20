### why we need kind   
* Virtual machine (take time, space it more worker nodes for each virtual machine)
* linux container (no need create vm and hypervisor)
### what is kind   
* It is a tool for running local Kubernetes clusters using Docker container “nodes”.   
* It is also called as kuberneties in docker.   
* Run kubernaties cluster entirely on docker container.   

###  how to set environment PATH 
1. Inline   
2. Internal   
3. Public    

**1. Inline**   
1. Use export command to set path.   
2. This setting is private to the terminal   
3. When current terminal is close then path set setting is remove    
Example `export PATH=$PATH:/usr/local/go/bin` 
**2. Internal**   
1. This setting is effect all the instance of terminal  
2. This setting add in the ~./bashrc file.  
3. Add same command Example `export PATH=$PATH:/usr/local/go/bin`     

**3. Public**   
1. This is system wide setting.  
2. After setting the path restart is mandatory.   
3. Example `sudo gedit /etc/environmant` 

### Setup kind with dependency  
1. install go tool  
2. install Docker   
3. How to configure kind  
```  
download golang tis is file name go1.15.6.linux-amd64.tar.gz
maaz@maaz-Lenovo-G50-70:~/github/GO$  tar zxf  go1.15.6.linux-amd64.tar.gz -C /usr/local  
maaz@maaz-Lenovo-G50-70:~/github/GO$  ls /usr/local
bin  etc  games  include  lib  man  sbin  share  src
maaz@maaz-Lenovo-G50-70:~/github/GO$ sudo !!
sudo tar zxf go1.15.6.linux-amd64.tar.gz -C /usr/local
[sudo] password for maaz: 
maaz@maaz-Lenovo-G50-70:~/github/GO$ sudo tar zxf go1.15.6.linux-amd64.tar.gz -C /usr/local  
maaz@maaz-Lenovo-G50-70:~/github/GO$ ls /usr/local
bin  etc  games  go  include  lib  man  sbin  share  src
```  
4.Set path for go  
``` 
maaz@maaz-Lenovo-G50-70:~/github/GO$ ls /usr/local
bin  etc  games  go  include  lib  man  sbin  share  src
maaz@maaz-Lenovo-G50-70:~/github/GO$ export PATH=$PATH:/usr/local/go/bin
maaz@maaz-Lenovo-G50-70:~/github/GO$ which go     
/usr/bin/go                            
but this is not wright the output is show like 
maaz@maaz-Lenovo-G50-70:~/github/GO$ which go   
usr/local/go/bin/go  
``` 
5. set kind path     
``` 
maaz@maaz-Lenovo-G50-70:~$ which go
/usr/bin/go
maaz@maaz-Lenovo-G50-70:~$ ls go/bin
kind
maaz@maaz-Lenovo-G50-70:~$ export PATH=$PATH:~/go/bin
maaz@maaz-Lenovo-G50-70:~$ which go
/usr/bin/go
maaz@maaz-Lenovo-G50-70:~$ ls go/bin
kind
maaz@maaz-Lenovo-G50-70:~$ which kind
/home/maaz/go/bin/kind
```               