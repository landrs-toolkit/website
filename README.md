# LANDRS Toolkit website source

This website uses Hugo and is based on https://git.okkur.org/syna-start

## To test Locally
The following describes how to create a development environment for this website. 
It assumes:
1. You have an operational installation of docker installed
2. You're using a linux host machine, but this should work fine for Windows/MacOS provided you adapt the commands accordingly
3. You have git credentials to push to the deployment [repo](ttps://github.com/landrs-toolkit/landrs-toolkit.github.io) (only required for deploying)


## Step1:
###  Select a location on host system to store website and make a docker volume point to it
```bash
$ mkdir WebsiteDev  #Or whatever you want to call it
$ cd WebsiteDev
$ git clone --recursive https://github.com/landrs-toolkit/website.git
```
## Step2:
### Fetch and build the docker image and start container.  
```bash
$ docker pull sewejaartjies/hugodev
$ docker run -it --rm --mount 'type=bind,src=<FullPathTo/WebsiteDev/website>,dst=/website' hugodev:latest   
```
Alternativly, if you can't pull from dockerhub you can build the image locally as follows.  Note this is only necessary if you failed to pull the image from dockerhub.  Once build completes successfull run the above ```docker run``` command as above.
```bash
$ cd website/docker
$ docker build --tag hugodev:latest .
```
This will put you into the container shell looking something like the following

## Step3
### Change into the mounted directory where the website source is and start the hugo server
```bash
$ root@<CONTAINER ID> 
$ root@<CONTAINER ID> cd /website                  
$ root@<CONTAINER ID> hugo serve -D       
```
## Step4
### In another terminal run the following to find the IP of the container you now have running:
```bash
$ docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <CONTAINER ID>
```

## Step5
### Website should be visible in a browser on host at \<IP\>:1313 Make whatever changes you need to the website

- When you're ready to deploy live run the following on the host machine from withing /WebsiteDev/website:

**--------------------------------NOTE: THIS WILL PUSH THE WEBSITE TO THE GITHUB LIVE REPO--------------------------------**
```bash
$ ./deploy.sh
```
It may take a few minutes to finish updating

-------------------------------------------------------------

## Notes on developing the website:
* To Set colours edit config.toml:
    * primary = "#ff6600"
    * secondary = "#868e96"
    * success = "#66ffff"
    * info = "#0066ff"
    * warning = "#9900cc"
    * danger = "#dc1200"
    * light = "#f8f9fa"
    * dark = "#343a40"
* To add new pages: make a new folder in content by coping and editing an existing example (eg contact)
* To add images for use everywhere in static/images, but if for use by a markdown page include in that resource folder (eg content/ddby/)
    * For storing images in the static directory, note that Syna fragments look for images in their own fragment directory, page directory and `static/images` directory. Read [image fallthrough documentation](https://syna.okkur.org/docs/image-fallthrough/) for more info.
* To include html content with its own style place folders in static
* To edit header and footer on all pages: content/_global

### Dev on front page specifically
- Edit main section:
    - Edit buttons, logo, opening text: \_index/hero.md
- Edit text in lower section: 
    - Make edits directly in html in: layouts/partials/fragments/sample-custom-fragment.html
- TODO: Currently subtitle text color is forced in themes/syna/layouts/partials/fragments/hero.html, should work out how to change properly using hugo template

### Directory Structure
```
├─ content/
|  └ _global/ # All global fragments are located in this directory
|  └ _index/ # Landing page is in this directory and it's url is changed to **/**.
|  └ about/ # About page
├ layouts/ # You can add extra layout files here. A sample custom fragment is available as a sample.
├ static/ # Your static files are in this directory.
├ themes/ # Hugo uses this directory as a default to look for themes. Syna theme is a git submodule available in this directory.
├ .gitignore
├ .gitmodules
├ config.toml # Hugo config file containing general settings and menu configs.
```
### Further details read Syna [full documentation](https://syna.okkur.org/docs).
