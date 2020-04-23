# Custom Markers

Grouping of similar/multiple test case can be done in pytest. Pytest allows us to use custom markers on test functions. To mark the test functions you can use the below decorator on the test functions
```
@pytest.mark.<markername>
```
And you can execute the marked test function with following option,
```
pytest -m <markername>
```

## PytestUnknownMarkWarning

Custom Markers should be registered before executing it. PytestUnknownMarkWarning will be emitted on use of unknown markers.

## Registering marks

You can register custom marks in your pytest.ini file like this:

```
[pytest]
markers =
    markername
```