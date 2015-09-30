# docker-piwik

### Preamble
Piwik, the open source analytics platform, MySQL and Nginx running in docker containers.
These containers require a small amount of up front configuration. Usage of HTTPS is require unless you want to make relatively significant changes to the nginx configuration.

You don't neccessarily have to use docker-compose, although if you're launching the containers manually via the Docker daemon you can use the docker-compose.yml file for an example of how to link the containers together and names to use.

### Configuration

#### Step 1. Clone the repository and all the submodules
The official Piwik github repository is included as a submodule in this repository. If you've never used git submodules before, [you can read about them here.](https://www.git-scm.com/book/en/v2/Git-Tools-Submodules)
To clone the full Piwik repository and all of *it's* submodules, use the following command:
```bash
git clone --recursive git@github.com:steelsage/docker-piwik.git
```
If you've already cloned the repository and forgot to use the --recursive flag, you can recursively clone submodules using the following command:
```bash
git submodule update --init --recursive
```

#### Step 2. HTTPS Configuration
You'll either need to buy an SSL certificate for the domain your intending to use, or [generate a self signed certificate.](http://www.akadia.com/services/ssh_test_certificate.html) You'll then need to install the certificate and private key for nginx to use:

- Create the directory ./certs at the base of the repository (it'll be ignored by the .gitignore file)
- Place your unencrypted private key at ./certs/piwik.key
- Place your certificate or certificate bundle at ./certs/piwik.crt
- Edit ./docker/nginx/piwik.conf and replace <YOUR_URL> with the URL you're intending to use for piwik

#### Step 3. Database configuration
You'll need to edit the ./docker/Dockerfile-mysql file and replace the variables with some strong passwords to be used for the root and standard database user respectively.

#### Step 4. Start with docker-compose
If you haven't yet, [install docker-compose.](https://docs.docker.com/compose/install/)
Running ```docker-compose up -d``` will build the images and start the application. You can use ```docker-compose logs``` to check that everything is working correctly.

#### Step 5. Run the Piwik configurator
Navigating to your chosen URL should show you the Piwik configuration / installation page. Simply follow the prompts to complete the installation.
