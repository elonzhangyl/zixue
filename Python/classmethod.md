+ classmethod
一个class只能指定一个输入参数*格式*，（比如只能接收某个指定的日期格式，这是class的*缺陷*），但实际使用中输入格式千变万化。解决这个矛盾最elegent的方式是classmethod。
boilerplate
```
class Date():

    def __init__(self, day, month, year):
        self.day = day
        self.month = month
        self.year = year

    @classmethod
    def from_string(cls, date_as_string):
        day, month, year = map(int, date_as_string.split('-'))
        date1 = cls(day, month, year)
        return date1
        
# normal usage,只能输入特定的日期格式
date1 = Date(11, 11, 2022)

# 如果日期格式该表，一个workaround是
string_date='11-11-2022'
day, month, year = map(int, string_date.split('-'))
date1 = Date(day, month, year)

# elegent
date2 = Date().from_string('11-09-2012')
```
Such function can be achieved by an independent method outside the class, but using classmethod allows a compact coding and fits OOP paradigm far better.
*classmethod的返回值一般是这个class的object*

+ staticmethod
