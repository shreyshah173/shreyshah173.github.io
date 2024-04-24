---
layout: post
title: Docker 3 Tier Architecture Tutorial!

---

hyy my name is shrey



0. **Setting Up the Full Stack Project**

   To deploy a Three-Tier Application using Docker, the initial step involves setting up a Full Stack Project. While any Full Stack Project can be utilized for this purpose, if one isn't available, an alternative project can be employed. In this instance, a straightforward project hosted on GitLab is utilized. The project, accessible via the link [developing-with-docker](https://gitlab.com/nanuchi/developing-with-docker), is constructed using HTML, CSS, JavaScript, Express, and MongoDB.

   To commence, clone the Project Repository using the following command:

   `git clone https://gitlab.com/nanuchi/developing-with-docker`


1. **Creating a Network for Docker Containers**

   To run a Three Tier Application, we need to run three Docker Containers simultaneously. So, it is necessary to run all these containers inside a network to avoid their interaction with other containers.

   So, Network can be created by using the following command after starting the Docker Engine with name mongo-network:

   ```bash
   docker network create mongo-network
   ```
   ![_config.yml]({{ site.baseurl }}/images/config.png)

![_config.yml]({{ site.baseurl }}/images/config.png)




working under here



Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.