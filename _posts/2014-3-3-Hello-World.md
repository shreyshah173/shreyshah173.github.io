---
layout: post
title: Docker 3 Tier Architecture Tutorial!

---

Hyy my name is shrey and this is my blog post 



0. **Setting Up the Full Stack Project**

   To deploy a Three-Tier Application using Docker, the initial step involves setting up a Full Stack Project. While any Full Stack Project can be utilized for this purpose, if one isn't available, an alternative project can be employed. In this instance, a straightforward project hosted on GitLab is utilized. The project, accessible via the link [developing-with-docker](https://gitlab.com/nanuchi/developing-with-docker), is constructed using HTML, CSS, JavaScript, Express, and MongoDB.

   To commence, clone the Project Repository using the following command:

   `git clone https://gitlab.com/nanuchi/developing-with-docker`

   ![_config.yml]({{ site.baseurl }}/images/clone.png)



1. **Creating a Network for Docker Containers**

   To run a Three Tier Application, we need to run three Docker Containers simultaneously. So, it is necessary to run all these containers inside a network to avoid their interaction with other containers.

   So, Network can be created by using the following command after starting the Docker Engine with name mongo-network:

   ```bash
   docker network create mongo-network
   ```
   ![_config.yml]({{ site.baseurl }}/images/config.png)


2. **Pulling and Running MongoDB Image**

   To pull the MongoDB image from DockerHub and run it as a container, execute the following command:
   ``` bash 
   docker run -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --network=mongo-network --name=21BCP335-mongodb -d mongo
   ```

   ![_config.yml]({{ site.baseurl }}/images/part3.png)

   Here, the `mongo` image will be automatically pulled from DockerHub to run the container in detachable mode with the name `21BCP335-mongodb` in the network `mongo-network`. The container will be running on the default port `27017`. You can check all the running containers using the command `docker ps`. Environment variables such as Username and Password are also passed to run the container. Similarly, we will be creating another container for Express by pulling its image from DockerHub.

3. **Running Express Container**

   The Express Container can be run using the following command:
   ``` bash 
   docker run -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password -e ME_CONFIG_MONGODB_SERVER=21BCP335-mongodb --network=mongo-network --name=21BCP335-express -d mongo-express
   ```

   ![_config.yml]({{ site.baseurl }}/images/part4.png)

   
   Here, the container with the name `21BCP335-express` is configured to connect the MongoDB Database with the Frontend of the project in Docker. The container will run on port `8081`. Environment variables such as Username and Password of the MongoDB are passed to access the Database, along with the container name of the MongoDB in the Server Environment variable. The container will be running on the same network as the previous container.

4. **Accessing the Frontend and Creating Databases**

   Next, open the following link in your browser: `localhost:8081`, and proceed to create two databases named `my-db` and `user-accounts`.

   ![_config.yml]({{ site.baseurl }}/images/part5.png)

   It's essential to create these two databases as they will be required by the Frontend during runtime. Additionally, make sure to update the MongoDB URL specified in the `server.js` file, as MongoDB will be running using Docker instead of on the Local Machine.

5. **Updating MongoDB URLs in the `server.js` File**

   Navigate to the `server.js` file within the project directory. Replace the values of `mongoUrlLocal` and `mongoUrlDocker` with the following MongoDB URL:

   ![_config.yml]({{ site.baseurl }}/images/part6.png)

   This step ensures that the server connects to the MongoDB database correctly. It replaces the previous URLs with the Docker-specific URL, allowing seamless integration with the MongoDB container running in Docker.


6. **Updating the Dockerfile**

   Next, delete the existing Dockerfile provided in the project. Then, create a new Dockerfile inside the `app` folder of the project using the following commands:

   ```Dockerfile
   FROM node
   WORKDIR /app
   COPY . .
   ENV MONGO_DB_USERNAME=admin
   ENV MONGO_DB_PWD=password
   RUN npm install
   EXPOSE 3000
   CMD ["node", "server.js"]
   ```

   ![_config.yml]({{ site.baseurl }}/images/part7.png)

7. **Building and Running the Docker Image**

   Open the Command Prompt (CMD) terminal inside the `app` folder of the project. Then, run the following command:

   ```bash
   docker build -t 21BCP335-project .
   ```
   ![_config.yml]({{ site.baseurl }}/images/part8.png)

   The execution of the above command will generate a Docker Image with name 21BCP335-project and it will take some time for it. After the Image is created we need to Run it as a Docker Container.

8. **Running the Docker Image as a Container**

   To run the Docker Image as a Docker Container, execute the following command:

   ```bash
   docker run -d -p 3000:3000 --network=mongo-network --name=21BCP335-project 21BCP335-project
   ```

   ![_config.yml]({{ site.baseurl }}/images/part9.png)

9. **Accessing the Webpage**

   Now, open the following link in your web browser: [localhost:3000](http://localhost:3000). You will be able to view the running webpage.

   ![_config.yml]({{ site.baseurl }}/images/part10.png)
   ![_config.yml]({{ site.baseurl }}/images/part11.png)
   ![_config.yml]({{ site.baseurl }}/images/part12.png)
   
   