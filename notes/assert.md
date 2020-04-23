# Assert
You can use the standard python assert for validation.

```
def test_01():
    assert 2 == 5
```

## Assert a Expected Exceptions
You can assert exception using below snippet,

```
with pytest.raises(Exception):
```

```
import pytest

def test_zero_division():
    with pytest.raises(ZeroDivisionError):
        5 / 0
```

