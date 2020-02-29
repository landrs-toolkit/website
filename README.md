# LANDRS Toolkit website source

This website uses Hugo and is based on https://git.okkur.org/syna-start

## To test Locally

### Prerequisites
- [Install Git](https://git-scm.com/downloads).
- [Install Go](https://golang.org/doc/install).
- [Install Hugo](https://gohugo.io/getting-started/installing/). Depending on your system, this might require Scoop, Choclatey, or other software. //Get the extended version 
- clone this repository recursively: 
```
$ git clone --recurse-submodules https://github.com/landrs-toolkit/website.git
```
- 
**Development testing**:
```
$ cd website
$ hugo server -D # This command starts the Hugo server and watches the site directory for changes.
```
Note: If running in a lxc container use:
```
$ hugo server --bind="0.0.0.0" -D
```
**Deploy live**:
```
$ ./deploy.sh
```

## Directory Structure

We're using the standard directory structure using content pages.

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

For storing images in the static directory, note that Syna fragments look for
images in their own fragment directory, page directory and `static/images`
directory. Read our [image fallthrough documentation](https://syna.okkur.org/docs/image-fallthrough/) for more info.

Further details read our [full documentation](https://syna.okkur.org/docs).

## First Steps

Open index.md and type. The changes are visible almost immediately at http://localhost:1313/.
