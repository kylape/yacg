# yacg - yet another code generation

The purpose of this project is to handle JSON schema models and generate
stuff based on them.

Possible use-case are for instance to create PlanUML class diagrams based
on the models, create bean classes based on model or more sophisticated
create fully dao code with included tests. 

Basically it's a tool to play with model driven development ...

The general workflow is:
1. Take a bunch of models - for this tool JSON schemas
2. Use some suitable templates
3. Feed all of them into the tool
4. yacg - processes templates and models
5. ... and produces different text outputs

Even if this tool written in Python it can be used to create text output
in every format - all depends from choosen templates.

To free the usage of yacg from too much care about dependencies, is on 
Docker Hub `https://hub.docker.com/repository/docker/okieoth/yacg/general` 
also a docker image, from the latest master brunch push, available. 

```bash
# pull the image
docker pull okieoth/yacg
```

# Usage
## Basic Usage

```bash
# basic preparation
pip install --user pipenv

pipenv --python 3.8
pipenv --three install
pipenv shell

# do a demo run
pipenv run python3 yacg.py \
    --models resources/models/json/yacg_config_schema.json \
             resources/models/json/yacg_model_schema.json \
    --singleFileTemplates plantUml=stdout

# run a test
pipenv run python3 -m unittest -v tests/model/test_model.py

# run all tests
pipenv run python3 -m unittest discover tests "test_*.py"
```
## Docker
```bash
# build a docker images
./bin/buildDockerImage.sh

# run the docker image
cd REPO_PATH
docker run -u $(id -u ${USER}):$(id -g ${USER}) -v `pwd`/resources:/resources --rm -t okieoth/yacg:0.13.0 \
    --models /resources/models/json/yacg_config_schema.json \
             /resources/models/json/yacg_model_schema.json \
    --singleFileTemplates plantUml=stdout

docker run -u $(id -u ${USER}):$(id -g ${USER}) -v `pwd`/resources:/resources --rm -t okieoth/yacg:0.13.0 \
    --models /resources/models/json/yacg_config_schema.json \
             /resources/models/json/yacg_model_schema.json \
    --singleFileTemplates xsd=stdout

```

# Documentation

## Mako templates
* Usage: https://docs.makotemplates.org/en/latest/usage.html
* Syntax: https://docs.makotemplates.org/en/latest/syntax.html

# Visual Studio Code
This project is written with vscode as editor. It contains also the .vscode configuration for the development.

Most interesting are in the debug section to pre-configured debugging tasks for the included tests.

* 'current tests' expects a open test file in the editor, and if this configuration is started, all test from this file are executed.
* 'all tests' let run all tests in the 'tests' folder of the repository

# Some Last Words
This project is a spare time project - with all its pros and cons. The development of 
project this project is done under a Linux OS, so I have no clue how it is working
on Windows machines. 
