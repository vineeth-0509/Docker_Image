FROM node:20           

WORKDIR /app

COPY . .

RUN npm install
RUN npm run build
RUN npx prisma generate

EXPOSE 3000
//all the above runs when we start or create the image.

CMD ["node", "dist/index.js"]
//all the above of cmd runs when we create an image
//whatever we have written after the cmd runs when we start the container.
//cmd means what will start after the container starts.


-> Do not allow the node modules into the docker file, either delete the node modules or create the .dockerignore file at the top level and add 
node_modules
dist
and all the things that we do not want to copy over to the docker file, add into the .dockerignore file

-> command is docker build -t backend .

//-t is the tag name that we want to give to it, we can name it according to the type of application we are creating.


//Run the docker
 docker run -p 3000:3000 backend(whatever the name that you have given)
docker push vineeth935/vineeth1_dockerimage:vineeth 

 volumes:
volumes are concepts that become importtant when we have multiple container running in which we have
->Need to persist data across docker restarts
->Need to allow containers to talk to each other

"whenever we start a mongodb container or a Database, its a good idea to attach a volume to it  ,because volume persists if the database or mongodb container crashes"

commands with volume:
1.Create a volume
docker volume create volume_database

->Mount the folder in mongo which actually stores the sata to this volume
docker run -v volume_database:/data/db -p 27017:27017 mongo
->/data/db is the folder where mongodb actually stores the data
->it eventually get persisted in the filesystem, the place where the data get persisted is the /data/db folder
-> whenever a container restarts

Networks:
In Docker, a network is a powerful feature that allows containers to communicate with each other and with the outside world
->Docker container can't talk to each other by default
->localhost on a docker container means it's own network, and not the network of the host machine

making container connected to each other using the network
-> There are many types of networks the most popular is the bridge network that we use to connect the multiple containers
1.Build the image
docker build -t image_tag .

1.Create a network
docker network create my-custom_network

1.start the backend process with teh network attached to it
docker run -p 3000:3000 --name backend --network my_custom_network image_tag

1.start mongo on the same network
docker run -d -v volume_database:/data/db --name mongo my_custom_network