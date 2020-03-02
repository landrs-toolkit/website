# LANDRS Toolkit website source

This website uses Hugo and is based on https://git.okkur.org/syna-start

## Dev notes:

- Set colours in config.toml:
    primary = "#ff6600"
    secondary = "#868e96"
    success = "#66ffff"
    info = "#0066ff"
    warning = "#9900cc"
    danger = "#dc1200"
    light = "#f8f9fa"
    dark = "#343a40"
- Add new pages: make a new folder in content by coping and editing an existing example (eg contact)
- Put images for use everywhere in static/images, but if for use by a markdown page include in that resource folder (eg content/ddby/)
- To include html content with its own style place folders in static
- Edit header and footer on all pages: content/_global

#### Dev on front page
    - Edit main section:
        - Edit buttons, logo, opening text: \_index/hero.md
    - Edit text in lower section: 
      -- Make edits directly in html in: layouts/partials/fragments/sample-custom-fragment.html
    - TODO: Currently subtitle text color is forced in themes/syna/layouts/partials/fragments/hero.html, should work out how to change properly using hugo template



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
