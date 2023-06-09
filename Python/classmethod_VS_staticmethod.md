+ 大总结
-一般的method定义一个instance的方法
- classmethod定义一个类的方法
- staticmethod定义一个跟instance也无关的方法（省空间，不用每个instance都有一个这个method的object）

-一般的method必须先经过__init__(), 但class method和staticmethod可以越过__init__()而直接调用，因而*可以预处理class的输入参数的格式*
+ classmethod
一个class只能指定一个输入参数*格式*，（比如只能接收某个指定的日期格式，这是class的*缺陷*），但实际使用中输入格式千变万化。解决这个矛盾最elegent的方式是classmethod。所有与这个类相关的方法都放在一起，而不是散落各地（好好好）。
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

    @staticmethod
    def is_date_valid(date_as_string):
        day, month, year = map(int, date_as_string.split('-'))
        return day <= 31 and month <= 12 and year <= 3999
        
# normal usage,只能输入特定的日期格式
date1 = Date(11, 11, 2022)

# 如果日期格式该表，一个workaround是
string_date='11-11-2022'
day, month, year = map(int, string_date.split('-'))
date1 = Date(day, month, year)

# elegent
date2 = Date().from_string('11-09-2012')

Date.is_date_valid('11-22-2222')

# 新增功能：
class Str2IntParam(Data_test):
    @classmethod
    def get_date(cls, string_date):
        #这里第一个参数是cls， 表示调用当前的类名
        year,month,day=map(int,string_date.split('-'))
        date1=cls(year,month,day)
        #返回的是一个初始化后的类
        return date1

```
Such function can be achieved by an independent method outside the class, but using classmethod allows a compact coding and fits OOP paradigm far better.
*classmethod的返回值一般是这个class的object*

+ staticmethod
也是对输入参数的前处理，但功能比classmethod少-不用涉及到class的调用.
It is a utility method and doesn't need an object ( self parameter) to complete its operation. So we declare it as a static method.
之所以叫做staticmethod，是因为他不会随着object的改变而改变。
