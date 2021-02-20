## Creating Image    
* There are two approaches to creating an image Using a running
1. container: a container is started and modifications are applied to the container.    
   From the container, docker commands are used to write modifications
2. Using a Dockerfile: a Dockerfile contains instructions for building an image. 
   Each instruction adds a new layer to the image, which offers more control over the files that are added to an image   
   at a later stage. dockerfile are basically script. 

## using dockerfile  
1. Dockerfile is a way to automate container builds.  
1. It contains all instructions required to build a container image.         
1. So instead of distributing images, you could just distribute the Dockerfile.  
1. Use `docker build.` to build the container image based on the Dockerfile in the current directory.    
1. `docker build . ` dot is used to see dockerfile in current directory.      
1. Images will be stored on your local system, but you can direct the image to be stored in a repository.    

   