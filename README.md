# Loan-repayment-plan

## 先计算还款周期
以按月付息为还款周期作为例子<br>
```python
import datetime
def gen_time_quarter(start, end, payment_day, period='1M'):
    res = []
    start_date=datetime.datetime.strptime(start,'%Y-%m-%d')
    end_date=datetime.datetime.strptime(end,'%Y-%m-%d')
    
    head = start_date
    flag = True
    tmp = start_date
    while start_date<end_date:
        if start_date.day == payment_day and (start_date-head).days > 15 and flag:
            res.append([head.strftime('%Y-%m-%d'), start_date.strftime('%Y-%m-%d')])
            head = start_date
            flag = False
            tmp = start_date
        elif start_date.day == payment_day and not flag:
            res.append([head.strftime('%Y-%m-%d'), start_date.strftime('%Y-%m-%d')])
            head = start_date
            tmp = start_date
        start_date = start_date + datetime.timedelta(days=1)
    if tmp < end_date:
        res.append([tmp.strftime('%Y-%m-%d'), end_date.strftime('%Y-%m-%d')])
    return res
  
get_time_quarter('2020-3-2','2020-3-14',15)
>>>[['2020-03-02', '2020-03-14']]
get_time_quarter('2020-3-2','2020-12-14',15)
>>>[['2020-03-02', '2020-04-15'],
 ['2020-04-15', '2020-05-15'],
 ['2020-05-15', '2020-06-15'],
 ['2020-06-15', '2020-07-15'],
 ['2020-07-15', '2020-08-15'],
 ['2020-08-15', '2020-09-15'],
 ['2020-09-15', '2020-10-15'],
 ['2020-10-15', '2020-11-15'],
 ['2020-11-15', '2020-12-14']]
