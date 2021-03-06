mturk-python
============

Complete Mechanical Turk API written in Python that uses the same names as the official documentation

mturk.py is a small library that sends requests to Mechanical Turk. It is much simpler than other libraries which redefine every function that Mechanical Turk recognizes. This saves you time so you don't have to worry about the library, just the Mechanical Turk API.

Read the official mTurk API docs [here](http://docs.aws.amazon.com/AWSMechTurk/latest/AWSMturkAPI/Welcome.html).

**Installation**

The library is compatible with both Python 2 and Python 3. You can install it using pip:

    pip install git+https://github.com/ctrlcctrlv/mturk-python.git


**Configuration**

The configuration settings can be passed as a dict to the `MechanicalTurk` constructor or saved in `mturkconfig.json` in the current working directory.

If you want to use a different name (or path), you can also specify that for the constructor: `mturk.MechanicalTurk(config_file='different_config_name.json')`

`stdout_log` enables the requests log of each request made to mTurk. `verify_mturk_ssl` verifies mTurk's SSL certificate. This should be left `true` in most cases, but according to bug reports it's broken on some operating systems.

```json
{
"use_sandbox" : false,
"stdout_log" : false,
"verify_mturk_ssl" : true,
"aws_key" : "ACCESSID",
"aws_secret_key" : "PASSWORD"
}
```
**Getting your balance**
```python
import mturk
m = mturk.MechanicalTurk()
r = m.request("GetAccountBalance")
if r.valid:
    print r.get_response_element("AvailableBalance")
```
**Assigning a qualification**
```python
import mturk
m = mturk.MechanicalTurk()
workers = ["A1ZZZ","A1QQQ"] # Replace these, of course!
for worker in workers:
    m.request("AssignQualification",
                {"QualificationTypeId":"2MYQUALIFICATION",
                 "WorkerId":worker, "IntegerValue":100})
```
If you find any bugs please open a new issue. 
