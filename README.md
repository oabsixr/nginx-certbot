# Boilerplate for nginx with Let’s Encrypt on docker-compose

> This repository is accompanied by a [step-by-step guide on how to
set up nginx and Let’s Encrypt with Docker](https://medium.com/@pentacent/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71).

`init-letsencrypt.sh` fetches and ensures the renewal of a Let’s
Encrypt certificate for one or multiple domains in a docker-compose
setup with nginx.
This is useful when you need to set up nginx as a reverse proxy for an
application, or when you need to spin up a simple web page.

## Installation
1. [Install docker-compose](https://docs.docker.com/compose/install/#install-compose).

2. In your working directory, clone this repository: `git clone https://github.com/oabsixr/nginx-certbot.git .`

3. Update the configurations as per requirements:
  
    ***a. Static web host - Modify configuration:***
    * Add domains and email addresses to init-letsencrypt.sh in lines 11, 12
    * Replace all occurrences of example.org with primary domain (the first one you added to init-letsencrypt.sh) in data/nginx/conf/app.conf

      `sed -i 's/example.org/<new domain name>/g' data/nginx/conf/app.conf`

    * Put website pages in data/html
      * eg. Update index.html to serve the content you want, or add static pages as necessary.
    
    ***b. Reverse proxy - Modify configuration:***
	* Add domains and email addresses to init-letsencrypt.sh in lines 11, 12
   * Replace all occurrences of example.org with primary domain (the first one you added to init-letsencrypt.sh) in data/nginx/conf/app.conf

      ```sed -i 's/example.org/<new domain name>/g' data/nginx/conf/app.conf```
	  
     
     
	* In data/nginx/conf/app.conf, look for the 'location /' code block and do the following: 
	  * comment out the 'root' instruction.
	  * uncomment the 'proxy_pass' instruction.
	  * update the value in proxy_pass to the url to proxy traffic to.
    
4. Run the init script:

    ```./init-letsencrypt.sh```

The site should now be up and running.


# Additional operational controls
## Stop the server:

    docker compose down

## Run the server:

    docker compose up


## License
All code in this repository is licensed under the terms of the `MIT License`. For further information please refer to the `LICENSE` file.
