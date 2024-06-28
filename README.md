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

-> command is docker build -t backend.

//-t is the tag name that we want to give to it, we can name it according to the type of application we are creating.


//Run the docker
 docker run -p 3000:3000 backend(whatever the name that you have given)
