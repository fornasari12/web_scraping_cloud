[![Python 3.8](https://github.com/fornasari12/aws_python_env/actions/workflows/main.yml/badge.svg)](https://github.com/fornasari12/aws_python_env/actions/workflows/main.yml)  [![Python 3.6](https://github.com/fornasari12/python_scaffold/actions/workflows/azure.yml/badge.svg)](https://github.com/fornasari12/python_scaffold/actions/workflows/azure.yml)


# Python Project Scaffold

[Link to Course repository](https://github.com/noahgift/scaffold)

<img width="788" alt="Screen Shot 2021-05-26 at 12 19 58" src="https://user-images.githubusercontent.com/57304126/119686453-b9c52980-be1c-11eb-8f62-c4b169e517ce.png">

### Connect to a GitHub repository with SSH keys and clone repository

```shell
# Press Enter to store the keys in home directory
echo "ssh"ssh-keygen -t rsa

# Print the key store in the directory.
cat /home/ec2-user/.ssh/id_rsa.pub

git clone git@github.com:fornasari12/aws_python_env.git
```

### Create required files.

```shell
touch Makefile
touch hello.py
touch test_hello.py
touch requirements.txt
```

### Create invisible Python virtual enviroment.

```shell
# create the venv with the same name of the repo
git remote -v

# create virtual env
python3 -m venv ~/.aws_python_env

# activate
source ~/.aws_python_env/bin/activate  
```

### Fill requirements

```
pylint
pytest
click
black
pytest-cov
```

### What is a Makefile and Why Do You Need it?

A common reaction to hearing about a Makefile from an absolute beginner to Python is, "why do I need this?".  Generally, it is healthy to have skepticism about things that appear to add work.  In the case of a Makefile, though, the reason to use them in a project is that they are less work because they keep track of complicated build steps that are very difficult to remember and type out correctly.

A great example is a lint step with the pylint tool.  With a Makefile, you only need to run:  make lint, and the same command can run inside a Continuous Integration server.  The alternative approach is to type out the full directive each time you need it, such as the following.

`pylint --disable=R,C *.py`

This sequence is very prone to errors and quite tedious to repeatedly typing over your project's life.  Instead, it is much simpler to type the following:

`make lint`

When you embrace the Makefile approach, it simplifies your workflow and makes it easier to integrate your project into a continuous integration system.  There is less code to type, and this is always a good thing for automation.  Further, Makefile commands are recognized by shell auto-completion, making it easy to "tab-complete" the steps.

Full Makefile example below:

```shell
install:
	pip install --upgrade pip &&\
		pip install -r requirements.txt

format:
	black *.py

lint:
	pylint --disable=R,C hello.py

test:
	python -m pytest -vv --cov=hello test_hello.py
```

# Review GitHub Actions GitHub Project


The `.github/workflows/pythonapp.yml` file stores the commands to build and test the project in GitHub Actions:

```yml
name: Python 3.8

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.8
      uses: actions/setup-python@v1
      with:
        python-version: 3.8
    - name: Install dependencies
      run: |
        make install
    - name: Lint with pylint
      run: |
        make lint
    - name: Test with pytest
      run: |
        make test
    - name: Format code
      run: |
        make format

```

