# flask-website

## Goal

The goal of this project is to create a flask website to allow students to login a portal and access their current stamps in order to redeem them for various prizes. In addition, we hope to implement a teacher's only portal where they can manage their student's stamps. 

## Our tech stack

Our tech stack is rather simple, as we are not using any front-end framework.

- Front-end: Jinja templates (Flask)
- Backend: Flask + SQLAlchemy
- Database: PostgreSQL

## How we are hosting this website

There's a lot of hosting providers available which makes it difficult and overwhelming to chose one. After some research, we settled on using Amazon Web Services (AWS) due to it's popularity and top-notch integration between their various services.

In particular, we chose to use the Elastic Beanstalk service, the CodePipeline service, and the Lightsail service.

### Overview (Elastic Beanstalk + managed vps database) 

Pros:
- Good git integration
- Separated database and back
- Easy database configuration
- Backups for database
- Easy web server configuration
Cons:
- (Maybe expensive)

### Elastic Beanstalk

The Elastic Beanstalk service is a great fit four our needs since we did not have to manually set up a web server with Nginx or Apache, but rather, we were able to select a Python pre-configured web server template. This helped us save time on configuration, which lets us focus on building our application. It also allows us to deploy our web application with ease thanks to it's integration to AWS CodePipeline, a service which deploys our app on every git push to the main branch where we host our code. 

### Our other choices

VPS standalone

    Pros:
        - Cheap
        - Only one place to login
        - Can install Dokku for git integration and set up Nginx 
    Cons:
        - Web server can be confusing to set up
        - Dokku might be difficult to set up
        - More problems to fix 
        - If the server crashes, everything goes down
        - No backups for database
    Options
        1. AWS lightsail Ubuntu
        2. Vultr
        3. DigitalOcean droplets

VPS + managed vps database

    Pros:
        - Separated database and backend
        - Easy database configuration
        - Can install Dokku for git integration and set up Nginx
        - Backups for database
    Cons:
        - More expensive than VPS standalone
        - Web server can be confusing to set up
        - Dokku might be difficult to set up
        - More problems to fix 

    Options
        1. AWS lightsail Ubuntu + AWS lightsail managed database
        2. Vultr + AWS lightsail managed database
        3. DigitalOcean droplets + DigitalOcean managed database
