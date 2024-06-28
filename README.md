FROM node:20           

WORKDIR /app

COPY . .

RUN npm install
RUN npm run build
RUN npx prisma generate

EXPOSE 3000
//all the above runns when we starting the image or creating the image.

CMD ["node","dist/index.js"]
//all the above of cmd runs when we create an image
//whatever we have written after the cmd runs when we start the container.
//cmd means what will statr after the container starts.


-> Donot allow the nodemodules in to the docker file, either delete the nodemodules or create the .dockerignore file at the top level add 
node_modules
dist
and all the things that we dont want to copy over to the docker file, add in to the .dockerignore file

-> command is: docker build -t backend .

//-t is what the tag name that we want to give to it, we can name according to our type of application that we are creating.


// run the docker
 docker run -p 3000:3000 backend(whatever the name that you have given)
docker push vineeth935/vineeth1_dockerimage:vineeth 

Networks and volumes:
Networks and volumes are concepts that become importtant when we have multiple container running in which we have
->Need to persist data across docker restarts
->Need to allow containers to talk to each other