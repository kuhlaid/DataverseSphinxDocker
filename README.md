# About this repository

This repository is derived from https://github.com/omnetpp/dockerfiles/tree/master/docker-sphinx. The purpose of this docker code is to create instructions needed to build Dataverse.org Sphinx documentation using Docker, with all required plugins, etc. defined in a Dockerfile script.

## Custom Sphinx Docker image

Within the root directory of this project, we will build a custom Sphinx Dataverse Docker Image (sddi); you can rename `sddi` whatever you want. Using the following command executes the Dockerfile script and builds our custom Sphinx image containing the required plugins (sphinx_bootstrap_theme and sphinx-icon):

```s (bash)
docker build -t sddi .`
```

### (this can be skipped) If you are new to Sphinx then you can use this
Then we use the Docker image we just built to create the Sphinx project template (`/mnt/q/testing/sphinxDocTest` is my local Sphinx project directory):

```s (bash)
docker run -it --rm -v /mnt/q/testing/sphinxDocTest:/docs sddi sphinx-quickstart
```

At this point we have a boilerplate `source` folder with some `hello world` documentation. We can copy the dataverse documentation source from the `dataverse\doc\sphinx-guides\source` GitHub directory and replace the boiler plate source directory Sphinx just created for us.

Last, we can make the Dataverse Sphinx documentation. ***Note the `/[project directory]:/docs` command below gives the impression that a `docs` folder should exist, but this is just standard Sphinx syntax and Sphinx will look through the `source` directory.***

```s (bash)
docker run --rm -v /mnt/q/testing/sphinxDocTest:/docs sddi make html
```

To see the documenation build, simply open the `build\html\index.html` file in your web browser.