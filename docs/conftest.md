# conftest.py

In your tests, if you have some fixtures are needs to be used for multiple test files then you can keep those fixtures in conftest.py file. You don’t need to import the fixture you want to use in a test, it automatically gets discovered by pytest. The discovery of fixture functions starts at test classes, then test modules, then conftest.py files and finally builtin and third party plugins.

Example:

conftest.py
```
import pytest

@pytest.fixture(autouse=True)
def initialize():
    print('initialize')
```

test_sample1.py
```
import pytest

def test_01():
    assert 2 == 2
```

test_sample2.py
```
import pytest

def test_02():
    assert 2 == 2
```

Run the above file,

```
pytest -s test_sample1.py test_sample2.py
```

```
Output
================
collected 3 items                                                                                                                                                                         

test_tc1.py . initialize                                                                                                                                                                      [ 33%]
test_tc2.py . initialize   

PASSED 
```

