# parametrize
parametrize to perform multiple calls to the same test function. Also it used to pass the input to the test and make the test drive by the input data. I.e. test will be executed in different instance for each input data.

## Example 1

```
import pytest

@pytest.mark.parametrize("i",[65,87,45,98,80])
def test(i):
    print(i)
    assert i>50
```
In the above example, test will be running for 5 times and thrid test which executes with data 45 will be failed but still the test continues for other input data

## Example 2

Example of multiple set of data passed to the test

```
import pytest

@pytest.mark.parametrize("uname,pword",[("test01","pw01"),("test02","pw02")])
def test(uname,pword):
    print(uname,pword)
```
In the above example, test will be running for 2 times and for every iteration two values will be passed

## Example 3

Example of parametrize with excel data driven

SampleFile.xlsx

![SampleFile](https://github.com/naveens33/pytest-tutorial/raw/master/docs/resources/excel_data.JPG)

read_data.py
```
import xlrd

def get_data():
    wb=xlrd.open_workbook("SampleFile.xlsx")
    sheet=wb.sheet_by_name("SheeName")
    data=[]
    for i in range(1,sheet.nrows):
        li=[]
        for j in range(0,sheet.ncols):
            li.append(sheet.cell_value(i,j))
        data.append(li)
    return data
```

test_sample.py
```
import pytest
from read_data import get_data

@pytest.mark.parametrize("name, addrs, acc, details",get_data())
def test_01(name, addrs, acc, details):
    print(name, addrs, acc, details)
```

In the above example, test will be running for 3 times and for every iteration each row values will be passed
