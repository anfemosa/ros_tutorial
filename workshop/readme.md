## Introduction

The workshop documents are written in `Markdown` language and built using [Sphinx](https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html?) documentation generator.

## Usage
### Install dependencies

````bash
cd ~/ros_tutorial/workshop/
python3 -m pip install -r requirements.txt
````

### To add new content
Place the content source in the following folders in the appropriate session.
-  `_source`: Markup (.md) files 
- `_static`: Images and other resource files  

Add the workshop's heading and filepath relative to `~/ros_tutorial/workshop/source/_source` to `index.rst`. To build the html:
 ````bash
 cd ~/ros_tutorial/workshop/
 make html
 ````
`index.rst` is built into `index.html` in the documentation output directory `~/ros_tutorial/workshop/build/html/index.html`. 

![docs](/workshop/source/_static/demo_rtd.png)


### Setup Docker for the workshops

To install `docker` on your `Ubuntu` system, follow the instructions ([here](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04). To use `docker` without `sudo`, make sure to follow the instructions in step 2, "Executing the Docker Command Without Sudo".