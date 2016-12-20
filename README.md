# Mongo

This is the official library of mongo builds for Singularity images hosted on Singularity Hub. The following standard applies:

 - each `Singularity` file corresponds to a build
 - the builds are organized by folders, with one `Singularity` file per folder. This ensures that we can find the files programatically.
 - the different image tags correspond to these folders, and the name of the tag is specified on Singularity Hub
 

## Local Generation
First, clone the repo.

      git clone https://www.github.com/singularituhub/mongo
      cd mongo/docker
      
Then, on your local machine, create an empty image for the mongo database

     sudo singularity create mongo.img
    
and use the build file `Singularity` to bootstrap the image:

     sudo singularity bootstrap mongo.img Singularity


## Running the Image
The entrypoint to communicate with mongo is accessible by running the image as an executable. Here is how to see the help commands:

      ./mongo.img --help

By default, since you likely won't have write access inside the image running on a cluster (the image itself is in read only mode) what we must do is map a local directory to store data. We can do that as follows:


       mkdir data  # this is your data directory on your local machine or cluster
       
       # In one terminal, we can start the database
       singularity run --bind $PWD/data:/data/db mongo.img --auth

       # And in another terminal, we can send a command to mongo, for example, connect
       singularity exec --bind $PWD/data:/data/db mongo.img mongo
         MongoDB shell version v3.4.0
         connecting to: mongodb://127.0.0.1:27017
         MongoDB server version: 3.4.0
         Welcome to the MongoDB shell.
         For interactive help, type "help".
         For more comprehensive documentation, see
	 http://docs.mongodb.org/
         Questions? Try the support group
	 http://groups.google.com/group/mongodb-user
         >


## Under Development
These images are currently not connected to Singularity Hub, but this will be done in early 2017. The first effort will be to develop a core set of images, and then any necessary builders / templating systems that would be necessary to help with this process. If you are interested in contributing, please [reach out](http://singularity.lbl.gov/contributing-code)!
