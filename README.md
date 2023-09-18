![Python package](https://github.com/gitpython-developers/GitPython/workflows/Python%20package/badge.svg)
[![Documentation Status](https://readthedocs.org/projects/gitpython/badge/?version=stable)](https://readthedocs.org/projects/gitpython/?badge=stable)
[![Packaging status](https://repology.org/badge/tiny-repos/python:gitpython.svg)](https://repology.org/metapackage/python:gitpython/versions)

## [Gitoxide](https://github.com/Byron/gitoxide): A peek into the future…

I started working on GitPython in 2009, back in the days when Python was 'my thing' and I had great plans with it.
Of course, back in the days, I didn't really know what I was doing and this shows in many places. Somewhat similar to
Python this happens to be 'good enough', but at the same time is deeply flawed and broken beyond repair.

By now, GitPython is widely used and I am sure there is a good reason for that, it's something to be proud of and happy about.
The community is maintaining the software and is keeping it relevant for which I am absolutely grateful. For the time to come I am happy to continue maintaining GitPython, remaining hopeful that one day it won't be needed anymore.

More than 15 years after my first meeting with 'git' I am still in excited about it, and am happy to finally have the tools and
probably the skills to scratch that itch of mine: implement `git` in a way that makes tool creation a piece of cake for most.

If you like the idea and want to learn more, please head over to [gitoxide](https://github.com/Byron/gitoxide), an
implementation of 'git' in [Rust](https://www.rust-lang.org).

## GitPython

GitPython is a python library used to interact with git repositories, high-level like git-porcelain,
or low-level like git-plumbing.

It provides abstractions of git objects for easy access of repository data often backed by calling the `git`
command-line program.

### DEVELOPMENT STATUS

This project is in **maintenance mode**, which means that

- …there will be no feature development, unless these are contributed
- …there will be no bug fixes, unless they are relevant to the safety of users, or contributed
- …issues will be responded to with waiting times of up to a month

The project is open to contributions of all kinds, as well as new maintainers.

### REQUIREMENTS

GitPython needs the `git` executable to be installed on the system and available in your `PATH` for most operations.
If it is not in your `PATH`, you can help GitPython find it by setting
the `GIT_PYTHON_GIT_EXECUTABLE=<path/to/git>` environment variable.

- Git (1.7.x or newer)
- Python >= 3.7

The list of dependencies are listed in `./requirements.txt` and `./test-requirements.txt`.
The installer takes care of installing them for you.

### INSTALL

GitPython and its required package dependencies can be installed in any of the following ways, all of which should typically be done in a [virtual environment](https://docs.python.org/3/tutorial/venv.html).

#### From PyPI

To obtain and install a copy [from PyPI](https://pypi.org/project/GitPython/), run:

```bash
pip install GitPython
```

(A distribution package can also be downloaded for manual installation at [the PyPI page](https://pypi.org/project/GitPython/).)

#### From downloaded source code

If you have downloaded the source code, run this from inside the unpacked `GitPython` directory:

```bash
pip install .
```

#### By cloning the source code repository

To clone the [the GitHub repository](https://github.com/gitpython-developers/GitPython) from source to work on the code, you can do it like so:

```bash
git clone https://github.com/gitpython-developers/GitPython
cd GitPython
git fetch --tags
./init-tests-after-clone.sh
```

If you are cloning [your own fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/about-forks), then replace the above `git clone` command with one that gives the URL of your fork. Or use this [`gh`](https://cli.github.com/) command (assuming you have `gh` and your fork is called `GitPython`):

```bash
gh repo clone GitPython
```

Having cloned the repo, create and activate your [virtual environment](https://docs.python.org/3/tutorial/venv.html). Then make an [editable install](https://pip.pypa.io/en/stable/topics/local-project-installs/#editable-installs):

```bash
pip install -e ".[test]"
```

In the less common case that you do not want to install test dependencies, `pip install -e .` can be used instead.

### Limitations

#### Leakage of System Resources

GitPython is not suited for long-running processes (like daemons) as it tends to
leak system resources. It was written in a time where destructors (as implemented
in the `__del__` method) still ran deterministically.

In case you still want to use it in such a context, you will want to search the
codebase for `__del__` implementations and call these yourself when you see fit.

Another way assure proper cleanup of resources is to factor out GitPython into a
separate process which can be dropped periodically.

#### Windows support

See [Issue #525](https://github.com/gitpython-developers/GitPython/issues/525).

### RUNNING TESTS

_Important_: Right after cloning this repository, please be sure to have
executed `git fetch --tags` followed by the `./init-tests-after-clone.sh`
script in the repository root. Otherwise you will encounter test failures.

On _Windows_, make sure you have `git-daemon` in your PATH. For MINGW-git, the `git-daemon.exe`
exists in `Git\mingw64\libexec\git-core\`; CYGWIN has no daemon, but should get along fine
with MINGW's.

#### Install test dependencies

Ensure testing libraries are installed. This is taken care of already if you installed with:

```bash
pip install -e ".[test]"
```

Otherwise, you can run:

```bash
pip install -r test-requirements.txt
```

#### Test commands

To test, run:

```bash
pytest
```

To lint, run:

```bash
pre-commit run --all-files
```

To typecheck, run:

```bash
mypy -p git
```

For automatic code formatting, run:

```bash
black git
```

Configuration for flake8 is in the `./.flake8` file.

Configurations for `mypy`, `pytest`, `coverage.py`, and `black` are in `./pyproject.toml`.

The same linting and testing will also be performed against different supported python versions
upon submitting a pull request (or on each push if you have a fork with a "main" branch and actions enabled).

### Contributions

Please have a look at the [contributions file][contributing].

### INFRASTRUCTURE

- [User Documentation](http://gitpython.readthedocs.org)
- [Questions and Answers](http://stackexchange.com/filters/167317/gitpython)
- Please post on Stack Overflow and use the `gitpython` tag
- [Issue Tracker](https://github.com/gitpython-developers/GitPython/issues)
  - Post reproducible bugs and feature requests as a new issue.
    Please be sure to provide the following information if posting bugs:
    - GitPython version (e.g. `import git; git.__version__`)
    - Python version (e.g. `python --version`)
    - The encountered stack-trace, if applicable
    - Enough information to allow reproducing the issue

### How to make a new release

- Update/verify the **version** in the `VERSION` file.
- Update/verify that the `doc/source/changes.rst` changelog file was updated.
- Commit everything.
- Run `git tag -s <version>` to tag the version in Git.
- _Optionally_ create and activate a [virtual environment](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment) using `venv` or `virtualenv`.\
(When run in a virtual environment, the next step will automatically take care of installing `build` and `twine` in it.)
- Run `make release`.
- Close the milestone mentioned in the _changelog_ and create a new one. _Do not reuse milestones by renaming them_.
- Go to [GitHub Releases](https://github.com/gitpython-developers/GitPython/releases) and publish a new one with the recently pushed tag. Generate the changelog.

### How to verify a release (DEPRECATED)

Note that what follows is deprecated and future releases won't be signed anymore.
More details about how it came to that can be found [in this issue](https://github.com/gitpython-developers/gitdb/issues/77).

----

Please only use releases from `pypi` as you can verify the respective source
tarballs.

This script shows how to verify the tarball was indeed created by the authors of
this project:

```bash
curl https://files.pythonhosted.org/packages/09/bc/ae32e07e89cc25b9e5c793d19a1e5454d30a8e37d95040991160f942519e/GitPython-3.1.8-py3-none-any.whl > gitpython.whl
curl https://files.pythonhosted.org/packages/09/bc/ae32e07e89cc25b9e5c793d19a1e5454d30a8e37d95040991160f942519e/GitPython-3.1.8-py3-none-any.whl.asc >  gitpython-signature.asc
gpg --verify gitpython-signature.asc gitpython.whl
```

which outputs

```bash
gpg: Signature made Fr  4 Sep 10:04:50 2020 CST
gpg:                using RSA key 27C50E7F590947D7273A741E85194C08421980C9
gpg: Good signature from "Sebastian Thiel (YubiKey USB-C) <byronimo@gmail.com>" [ultimate]
gpg:                 aka "Sebastian Thiel (In Rust I trust) <sebastian.thiel@icloud.com>" [ultimate]
```

You can verify that the keyid indeed matches the release-signature key provided in this
repository by looking at the keys details:

```bash
gpg --list-packets ./release-verification-key.asc
```

You can verify that the commit adding it was also signed by it using:

```bash
git show --show-signature  ./release-verification-key.asc
```

If you would like to trust it permanently, you can import and sign it:

```bash
gpg --import ./release-verification-key.asc
gpg --edit-key 4C08421980C9

> sign
> save
```

### Projects using GitPython

- [PyDriller](https://github.com/ishepard/pydriller)
- [Kivy Designer](https://github.com/kivy/kivy-designer)
- [Prowl](https://github.com/nettitude/Prowl)
- [Python Taint](https://github.com/python-security/pyt)
- [Buster](https://github.com/axitkhurana/buster)
- [git-ftp](https://github.com/ezyang/git-ftp)
- [Git-Pandas](https://github.com/wdm0006/git-pandas)
- [PyGitUp](https://github.com/msiemens/PyGitUp)
- [PyJFuzz](https://github.com/mseclab/PyJFuzz)
- [Loki](https://github.com/Neo23x0/Loki)
- [Omniwallet](https://github.com/OmniLayer/omniwallet)
- [GitViper](https://github.com/BeayemX/GitViper)
- [Git Gud](https://github.com/bthayer2365/git-gud)

### LICENSE

[New BSD License](https://opensource.org/license/bsd-3-clause/). See the [LICENSE file](https://github.com/gitpython-developers/GitPython/blob/main/license).

[contributing]: https://github.com/gitpython-developers/GitPython/blob/main/CONTRIBUTING.md
[license]: https://github.com/gitpython-developers/GitPython/blob/main/license
