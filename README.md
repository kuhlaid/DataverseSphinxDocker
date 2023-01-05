# About this repository

This repository is derived from https://github.com/omnetpp/dockerfiles/tree/master/docker-sphinx. The purpose of this docker code is to create instructions needed to build Dataverse.org Sphinx documentation using Docker, with all required plugins, etc. defined in a Dockerfile script.

## Custom Sphinx Docker image to build HTML

Within the root directory of this project, we will build a custom Sphinx Dataverse Docker Image (sddi_html); you can rename `sddi_html` whatever you want. Using the following command executes the Dockerfile script and builds our custom Sphinx image containing the required plugins (sphinx_bootstrap_theme and sphinx-icon):

```s (bash)
cd /mnt/q/GitHubRepos/DataverseSphinxDocker/SphinxDocBuildHtml
docker build -t sddi_html .
```

### (this can be skipped) If you are new to Sphinx then you can use this to create `make` files and a sample `source` directory with sample documents
Then we use the Docker image we just built to create the Sphinx project template (`/mnt/q/GitHubRepos/DataverseSphinxDocker` is my local Sphinx project directory):

```s (bash)
docker run -it --rm -v /mnt/q/GitHubRepos/DataverseSphinxDocker:/docs sddi_html sphinx-quickstart
```

At this point we have a boilerplate `source` folder with some `hello world` documentation. We can copy the dataverse documentation source from the `dataverse\doc\sphinx-guides\source` GitHub directory and replace the boiler plate source directory Sphinx just created for us.

Last, we can make the Dataverse Sphinx documentation. ***Note the `/[project directory]:/docs` command below gives the impression that a `docs` folder should exist, but this is just standard Sphinx syntax and Sphinx will look through the `source` directory.***

```s (bash)
docker run --rm -v /mnt/q/GitHubRepos/DataverseSphinxDocker:/docs sddi_html make html
```

To see the documenation build, simply open the `build\html\index.html` file in your web browser.

## To build a PDF from the source

Build a Docker image with Sphinx and Latex (we will call it `sddi_pdf` so we do not confuse it with the Sphinx image for building the HTML).

```s (bash)
cd /mnt/q/GitHubRepos/DataverseSphinxDocker/SphinxDocBuildPDF
docker build -t sddi_pdf .
```

Make the 

```s (bash)
docker run --rm -v /mnt/q/GitHubRepos/DataverseSphinxDocker:/docs sddi_pdf make latexpdf
```