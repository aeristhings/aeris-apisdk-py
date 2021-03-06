# aeris-apisdk-py
This package is intended to provide both an SDK and CLI for the Aeris connectivity APIs. It can also serve as sample code for customers to write their own integrations to Aeris APIs.

This is not production code. There is no formal support provided by Aeris for this SDK.


## Getting Started - Aeris API Documentation

You may find information about the Aeris connectivity APIs [here](https://aeriscom.zendesk.com/hc/en-us/categories/360002203434).


## Getting Started - Install Package

If you want to install and use the package rather than make changes to it, see:

https://github.com/aeristhings/aeris-apisdk-py/wiki

## Getting Started - Development

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What you need to develop and test.

What I'm using:

```
git --version = 2.17.1
python --version = 3.7.5
pip --version = 19.3.1
poetry --version = 1.0.0
```

### Installing

A step by step series of examples that tell you how to get a development env running

Step 1: Clone the source to your local machine

```
$ git clone https://github.com/aeristhings/aeris-apisdk-py.git

Cloning into 'aeris-apisdk-py'...
remote: Enumerating objects: 38, done.
remote: Counting objects: 100% (38/38), done.
remote: Compressing objects: 100% (36/36), done.
remote: Total 38 (delta 12), reused 14 (delta 0), pack-reused 0
Unpacking objects: 100% (38/38), done.
```

Step 2: Install dependencies

```
$ cd aeris-apisdk-py
$ poetry install

Updating dependencies
Resolving dependencies... (0.9s)

Writing lock file


Package operations: 18 installs, 0 updates, 0 removals

  - Installing more-itertools (8.1.0)
  - Installing zipp (1.0.0)
  - Installing importlib-metadata (1.4.0)
  - Installing pyparsing (2.4.6)
  - Installing six (1.13.0)
  - Installing attrs (19.3.0)
  - Installing certifi (2019.11.28)
  - Installing chardet (3.0.4)
  - Installing idna (2.8)
  - Installing packaging (20.0)
  - Installing pluggy (0.13.1)
  - Installing py (1.8.1)
  - Installing urllib3 (1.25.7)
  - Installing wcwidth (0.1.8)
  - Installing click (7.0)
  - Installing pathlib (1.0.1)
  - Installing pytest (5.3.2)
  - Installing requests (2.22.0)
```

Step 3: Verify development environment working

```
$ poetry run aeriscli

Usage: aeriscli [OPTIONS] COMMAND [ARGS]...

Options:
  -v, --verbose             Verbose output
  -cfg, --config-file TEXT  Path to aservices config file.
  --help                    Show this message and exit.

Commands:
  aeradmin    AerAdmin API Services
  aerframe    AerFrame API Services
  aertraffic  AerTraffic API Services
  config      Set up the configuration for using this tool
```



## Running the tests

This section covers the automated tests for this system

### Functional tests

This project uses pytest for running functional tests

```
$ poetry run pytest
============================= test session starts ==============================
platform linux -- Python 3.7.5, pytest-5.3.2, py-1.8.1, pluggy-0.13.1
rootdir: ~/aeris-apisdk-py
collected 54 items                                                             

tests/test_aeradminsdk.py ......                                         [ 11%]
tests/test_aerframesdk.py .............................................. [ 96%]
.                                                                        [ 98%]
tests/test_aerisapisdk.py .                                              [100%]

============================== 54 passed in 0.41s ==============================
```

### Coding style tests

This project used pycodestyle to ensure adherence to PEP 8 coding style rules.

Running pycodestyle as below should return with no errors.

```
$ poetry run pycodestyle --max-line-length=120 aerisapisdk/ tests/
```

### Integration tests

To specify your own Aeris API endpoints, create a configuration file that contains a JSON object with the key "urls" and value an object with keys

* aerframe_ws_api
* aerframe_lp_api
* aeradmin_api
* aertraffic_api

Then, either use the `--config-file` argument to the `aeriscli` command, or the `aerisapisdk.aerisconfig.load_config` method to load that file.


## Releasing

This section covers release activities.

### Changelog

Make sure there is an entry in the [CHANGELOG](https://github.com/aeristhings/aeris-apisdk-py/blob/master/CHANGELOG.md) for the version you will release.
Included should be the git tag for the release, new features added, and bugs fixed. If relevant, it should also include notes about upgrade and security issues.

### Updating the Version Number
Before you build and publish, you will need to make sure that the version is changed so that users can easily pick up the latest version.

You can easily do that via poetry. For example, to increment the patch-level version, issue the command:

```
$ poetry version patch
Bumping version from 0.1.4 to 0.1.5
```


### Building
You can use poetry to build the distribution that we will want to publish to pypi.org. Use the 'build' command.

I have not found a way to clean out the previous build distribution. You may have to manually 'rm -rf dist' to remove before running the build.

```
$ poetry build
Building aerisapisdk (0.1.3)
 - Building sdist
 - Built aerisapisdk-0.1.3.tar.gz

 - Building wheel
 - Built aerisapisdk-0.1.3-py3-none-any.whl
```

### Publishing
The publish command uploads to pypi.org so that users can install via 'pip install' or 'pip install --upgrade'.

```
$ poetry publish

Publishing aerisapisdk (0.1.3) to PyPI
Username: <myusername>
Password:
 - Uploading aerisapisdk-0.1.3-py3-none-any.whl 100%
 - Uploading aerisapisdk-0.1.3.tar.gz 100%
```

### Tagging
Finally, tag the master branch with the version and push that tag.

Use the format `v(major).(minor).(patch)` for the tag. Example: for release 0.1.5, the tag would be "v0.1.5"


### Testing the Publishing Process
test.pypi.org is a test version of pypi.org. Once you have built the package (see "Building," above), you can use these instructions to test the release process. This is useful for testing PyPI's display of project metadata, such as the classifiers.

1. Create an account on https://test.pypi.org/
2. Verify your email address
3. Add the test repository (named "test" in these examples) to Poetry:
    1. `$ poetry config repositories.test https://test.pypi.org/legacy/`
4. Configure credentials for the test repository:
    1. `$ poetry config http-basic.test your_test.pypi.org_username your_test.pypi.org_password`
5. Publish to the test repository:
    1. `$ poetry publish -r test`


## Built With

* [Poetry](https://python-poetry.org/) - Python dependency management
* [Click](https://click.palletsprojects.com/en/7.x/) - Python package for creating beautiful command line interfaces
* [pytest](https://docs.pytest.org/en/latest/) - Python testing tool that helps you write better programs
* [pycodestyle](http://pycodestyle.pycqa.org/en/latest/index.html) -  A tool to check Python code against the style conventions in PEP 8

## Contributing

Please read [CONTRIBUTING.md](https://github.com/aeristhings/aeris-apisdk-py/blob/master/CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/aeristhings/aeris-apisdk-py/tags). 

## Authors

* **Drew Johnson** - *Initial work*

See also the list of [contributors](https://github.com/aeristhings/aeris-apisdk-py/contributors) who participated in this project.

## License

This project is licensed under the Apache 2.0 License - see the [LICENSE](https://github.com/aeristhings/aeris-apisdk-py/blob/master/LICENSE) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
