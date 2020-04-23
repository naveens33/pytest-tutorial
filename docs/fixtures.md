# Fixtures
Fixtures are the functions to run before test function. Also, it helps to feed data to the test function and act as dependencies.

## Basic Fixture function
To make a function as a fixture, you need to mark that function below with the marker
```
@pytest.fixture
def initialize():
    print("initialize")
```
## Ways to apply fixture to the test function

1. name it in test function parameter
2. usefixtures decorator
3. autouse

Follow the below example,

### 1. name it in test function parameter:

```
import pytest

@pytest.fixture
def initialize():
    print("initialize")

def test_01(initialize):
    print("test_01")
```

### 2. usefixtures decorator

```
import pytest

@pytest.fixture
def initialize():
    print("initialize")

@pytest.mark.usefixtures("initialize")
def test_01():
    print("test_01")
```

### 3. autouse
autouse is the optional parameter to the fixture decorator. The default value is False, such that the fixture cannot be applied to the test function. If you provide True then it will automatically apply to the test function.

Note: autouse will apply to the test function as per the scope of the fixture. The default scope of fixture is "function". Please go through the parameter section of fixture decorator to learn more about the scope.

```
import pytest

@pytest.fixture(autouse=True)
def initialize():
    print("initialize")

def test_01():
    print("test_01")
```

## Parameters of fixture decorator

### 1. scope
scope defines how often the fixture gets called. Following are options for scope,
```
function   - Run once per test function
class      - Run once per class
module     - Run once per module
session    - Run once per session
```
Note: Higher-scoped fixtures are instantiated first

### 2. params
an optional list of parameters which will cause multiple invocations of the fixture function and all of the tests using it. The current parameter is available in ```request.param```.

```
import pytest

@pytest.fixture( params=[
    ("username1","password1"),
    ("username2","password2"),
    ("username3","password3")
] )
def initialize(request):
    print(request.param[0],request.param[1])
```

In the above example, that fixture is invoked multiple times as many parameter we have provide. I.e. initialize fixture runs for thrice and the data from the parameter can be received/get using ```request.param```

### 3. autouse
Please go through the ```Ways to apply fixture to the test function``` section

## Return from fixture

Fixtures can feed data to the test function and act as dependencies with the help of return statement

For example,

```
import pytest

@pytest.fixture
def input_value():
    age = 56
    return age

def test_01(input_value):
    assert input_value >= 18
```

## Add cleanup/teardown code to the fixture
Cleanups or teardown to the fixtures can be achived in below ways,

### 1. Using yield
By using a yield statement instead of return, all the code after the yield statement serves as the teardown,

```
import pytest

@pytest.fixture
def initialize():
    print('initialize')

    yield
    print('cleanup')

def test_01(initialize):
    print('test_01')

Output
================
test_sample.py::test_01 

initialize
test_01
cleanup
PASSED                                           [100%]
```

### 2. Using addfinalizer method

An alternative option for executing teardown code is to make use of the addfinalizer method of the request-context object to register finalization functions.

```
import pytest

@pytest.fixture
def initialize(request):
    print('initialize')
    
    def fin():
        print("cleanup")
    
    request.addfinalizer(fin)

def test_01(initialize):
    print('test_01')

Output
================
test_sample.py::test_01 

initialize
test_01
cleanup
PASSED                                           [100%]
```

One benefit of addfinalizer method is, you can use return statement incase if your test requires any input from the fixture

Example:
```
import pytest

@pytest.fixture
def input_value(request):
    age = 56

    def fin():
        print("cleanup")

    request.addfinalizer(fin)
    return age

def test_01(input_value):
    assert input_value >= 18
```

## Example 1

Selenium Webdriver script with pytest fixture - Login Scenario

```
import pytest
from selenium import webdriver

@pytest.fixture(scope="session", autouse=True)
def driver(request):
    driver_ = webdriver.Chrome(r"D:/Naveen/Selenium/chromedriver_win32/chromedriver.exe")
    driver_.maximize_window()
    driver_.get("http://zero.webappsecurity.com")

    def quit():
        driver_.quit()

    request.addfinalizer(quit)
    return driver_

def test_login(driver):
    driver.find_element_by_id('signin_button').click()
    driver.find_element_by_id('user_login').send_keys('username')
    driver.find_element_by_id('user_password').send_keys('password')
    driver.find_element_by_name('submit').click()
    assert driver.title == 'Account Summary'
```

## Multiple Fixtures
You can use multiple fixture to the test.

Example:

```
import pytest

@pytest.fixture
def input_name():
    name = "Bob"
    return name

@pytest.fixture
def input_age():
    age = 56
    return age

def test_01(input_name, input_age):
    print(input_name, input_age)
```

Note: Higher-scoped fixtures are instantiated first.

I.e. in the below example you can see input_age() has scope - session and input_name() has default scope function. Since session scope is the highest one so, input_age() executed first. Verfiy the output


```
import pytest

@pytest.fixture
def input_name():
    print("1st")
    name = "Bob"
    return name

@pytest.fixture(scope="session")
def input_age():
    print("2nd")
    age = 56
    return age

def test_01(input_name, input_age):
    print(input_name, input_age)

Output
================
test_sample.py::test_01 
2nd
1st
Bob 56
PASSED 
```

## Chain the fixtures

Fixtures themselves can also use one or more fixtures. Such that you can chain the fixtures

Example:

```
import pytest

@pytest.fixture
def first():
    print("first")

@pytest.fixture
def second(first):
    print("second")

def test_01(second):
    print("test_01")

Output
================
test_sample.py::test_01 
first
second
test_01
PASSED 
```