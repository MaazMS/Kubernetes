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
2. This setting is private to the terminal.   
3. When current terminal is close then path set setting is remove.      
Example `export PATH=$PATH:/usr/local/go/bin`        
    
**2. Internal**   
1. This setting is effect all the instance of terminal  
2. This setting add in the ~./bashrc file.  
3. Add same command Example `export PATH=$PATH:/usr/local/go/bin`     

**3. Public**   
1. This is system wide setting.  
2. After setting the path restart is mandatory.   
3. open the file where we set environment path `sudo gedit /etc/environmant`    
`/home/maaz/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:`
4. This path already available then we add go path using colon and path location.     
Example    
`/home/maaz/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/local/go/bin`            
    

### Setup kind with dependency  
1. install go tool  
2. install Docker   
4. download kind     
3. How to configure kind      

**install go tool and download kind**  
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
**Note**download kind   
maaz@maaz-Lenovo-G50-70:~$ GO111MODULE="on" go get sigs.k8s.io/kind@v0.9.0
```  
4.Set path for go  
``` 
maaz@maaz-Lenovo-G50-70:~/github/GO$ ls /usr/local
bin  etc  games  go  include  lib  man  sbin  share  src
maaz@maaz-Lenovo-G50-70:~/github/GO$ export PATH=$PATH:/usr/local/go/bin
maaz@maaz-Lenovo-G50-70:~/github/GO$ which go   
usr/local/go/bin/go                             
but this is not working in my ubuntu the output is show like 
maaz@maaz-Lenovo-G50-70:~/github/GO$ which go     
/usr/bin/go
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