# Mongo

This is an example of building a mongo container with Singularity.


## Local Generation
First, clone the repo.

```bash
git clone https://www.github.com/singularityhub/mongo
cd mongo
```
      
Then, on your local machine, build the container!

```bash
sudo singularity build mongo.sif Singularity
```

## Running the Image

The entrypoint to communicate with mongo is accessible by running the image as an executable. Here is how to see the help commands:

```bash
./mongo.sif --help
```

By default, since you likely won't have write access inside the image running on a cluster (the image itself is in read only mode) what we must do is map a local directory to store data. We can do that as follows:

```bash
mkdir data  # this is your data directory on your local machine or cluster
```

In one terminal, we can start the database

```bash
singularity run --bind $PWD/data:/data/db mongo.sif --auth
```

And in another terminal, we can send a command to mongo, for example, connect

```bash
$ singularity exec --bind $PWD/data:/data/db mongo.sif mongo
MongoDB shell version v4.2.1
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("22992c09-84bd-416c-9934-db7145a5d37c") }
MongoDB server version: 4.2.1
> 
```
