skip, skipif and xfail are built-in markers for test function

##  skip

skip marker is used to skip the particular test with some reason provided

```
import pytest

@pytest.mark.skip("Not yet developed")
def test_01():
    print("test01")

Output
================
Skipped: Not yet developed
```

## skipif

skip the test function by validating a condition

```
import sys
import pytest

@pytest.mark.skipif(sys.platform == 'win32',reason="This test not will be executed in windows os")
def test_01():
    print("test01")
    
Output
================
Skipped: This test not will be executed in windows os
```

## Skip test using pytest.skip function
Skip an executing test with the given message.
```
    def test_02():
        pytest.skip("Not Yet Developed")
```


## xfail

xfail marker is used to indicate that the particular test is expect to be fail.

```
import pytest

@pytest.mark.xfail
def test_01():
    print('test01')
```
This test will run but no traceback will be reported when it fails.
