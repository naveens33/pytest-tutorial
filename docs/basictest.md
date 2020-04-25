# Create First Test
pytest discover the test by its standard convention. Below are the standard conventions,

Files - test_*.py or *_test.py files

Functions or Method - test_ prefixed test functions or methods outside of class

Class - Test_ prefixed test classes

##  Write a sample pytest test

test_sample.py
```
def test_01():
    assert 5==5
```

## Execute the pytest test

You can execute the pytest test in different ways,

### 1. Using Pycharm Configuration.

If you are using Pycharm to create and maintain your test, you can follow the below steps to execute the test

Once the test_sample.py file and test_01 function is created.

* Go to File -> Settings -> Tools -> Python Integrated Tools
* Under Testing choose Default test runner as pytest
* Now, Right click on the editor and you can find **Run 'pytest for test_sample'**

### 2. Using commands in the terminal

You can run your pytest test using below command,

```
pytest [options] [file_or_dir] [file_or_dir]
```
Also pytest provides plenty of command line options to select and run the test.

Refer [Command line Options](https://github.com/naveens33/pytest-tutorial/blob/master/docs/commandlineoptions.md)

### 3. Using configuration file

pytest look for pytest.ini, tox.ini and setup.cfg configuration file to execute the test.

```
[pytest]
python_files =
    test_sample.py
```


