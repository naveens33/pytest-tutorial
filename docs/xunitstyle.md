# Classic xunit-style fixtures

pytest support classic xunit-style of fixtures like setup and teardown.

Depending on the scope you can define setup/teardown fixtures,

|Scope|xunit-style Fixtures|Description|
|-----|--------|-----------|
|Module Level| setup_module/teardown_module|Run once before the module/Run once after the module|
|Class Level| setup_class/teardown_class|Run once before the class/Run once after the class|
|Method Level|setup_method/teardown_method|Run once before the method/Run once after the method|
|Function Level|setup_function/teardown_function|Run once before the function/Run once after the function|

Note: While these setup/teardown methods are simple and familiar to those coming from a unittest or nose background, you may also consider using pytest’s more powerful fixture mechanism which leverages the concept of dependency injection, allowing for a more modular and more scalable approach for managing test state, especially for larger projects and for functional testing.

Example:
```
def setup_module(module):
    print('setup_module')


def teardown_module(module):
    print('teardown_module')


def setup_function(function):
    print('setup_function')


def teardown_function(function):
    print('teardown_function')


def test_01():
    print('-  test01')


def test_02():
    print('-  test02')


class TestClass:

    @classmethod
    def setup_class(cls):
        print('setup_class')

    @classmethod
    def teardown_class(cls):
        print('teardown_class')

    def setup_method(self, method):
        print('setup_method')

    def teardown_method(self, method):
        print('teardown_method')

    def test_03(self):
        print('- test03')

    def test_04(self):
        print('- test04')
        
 Output
================
collecting ... collected 4 items
test_sample.py::test_01 
setup_module
setup_function
PASSED                                              [ 25%]-  test01
teardown_function

test_sample.py::test_02 
setup_function
PASSED                                              [ 50%]-  test02
teardown_function

test_sample.py::TestClass::test_03 
test_sample.py::TestClass::test_04 

setup_class
setup_method
PASSED                                   [ 75%]- test03
teardown_method
setup_method
PASSED                                   [100%]- test04
teardown_method
teardown_class
teardown_module
PASSED 
```