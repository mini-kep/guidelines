Testing requirements 
====================

- Tests in the project use [pytest](https://docs.pytest.org/en/latest/), 
  [Travis CI](https://travis-ci.org/mini-kep/) and [codecov](https://codecov.io/gh/mini-kep/).
- Tests cover at least all public methods/functions.
- Tests are assembled by test class for every single class under test.

Each test:

1. has a long descriptive name based on a pattern ```test_<WHAT1>_on_<WHAT2>_<DOES_WHAT>```:
   - `<WHAT1>` name of function/method name under test, eg `upload`, `upload_method`, `status_property`
   - `<WHAT2>` context/condition or arguments, eg `on_negative_integer`, `on_init`, `on_teardown` 
   - `<DOES_WHAT>` expected result or behaviour, eg `returns_none`, `raises_error` 
   - regrassion tests / bugfixes are named based on behaviour
2. addresses one issue and preferably has one assert per test
3. has clear separation of setup, call of code under test and result check 

When experiencing problems with tests design, comment your test using [format below]()
and submit for review.

Testing guidelines
==================

These guidelines cover unit tests in ```mini-kep``` project.

Here we do not describe functional (eg selenium) or load tests, which may have different logic. 

Introduction
------------

Testing is known to be even harder than writing original code. 

When testing one must think of:

a) program behaviours
- how the code under test is supposed to run well 
- how the code under test may run with error
- how to simulate good and bad behaviours in test setup and checks?
- what happens in program outside code under test?

b) clean tests
- how to write test in a clean and understandable fashion? 
- how to name tests?
- how to make tests small?

c) test efficiency
- what conditions/arguements/contexts are most probable for the code under test?
- what if the first thing should I test for?
- how would readers inderstand what the test code does?


What is special about unittests?
--------------------------------

We treat unit tests as a tool to control program structure. They must 
fail early and indicate what has changed in the code under test. 

Unittests are 'example tests', it is costly to use them 
to validate all program behaviour. Even with a lot of unittests 
validation is never complete. 

Design your unit tests around:
   - method/function interface  
   - primitive success outcomes
   - propaple risks in program excution
  
You can make tests more exaustive by using parametrisation/randomisation 
of unttests or swithiching to integration/acceptance tests. 
These types of tests are different from unittests, even though may 
use similar libraries. 

Beware of [dirty hybrids](http://blog.stevensanderson.com/2009/08/24/writing-great-unit-tests-best-and-worst-practises) - 
tests that are stuck in the middle of unit test and integration test. They ususaly require complex setup and 
complex checks, and very hard to maintain. You should not do such tests, unless you have a special reason.  

Checklist
----------

#### Recommendations:

Best tests:
- run quick and often
- use a continious integration like Travis CI and use coverage metrics like codecov 
- are as simple and readable as they can get, nobody can simplify them further
- fail early and near to where problem is
- concentrate around practical risks in program execution, not fantasy situations  
- make good use of test class inheritance, parametrisation/randomisation, factories/fixtures, dependency injection, mocks and monkey-patching
- include just a few integration, end-to-end tests
- are isolated one from another
- they have no more than 5-7 lines of code 
- can be reproduced just by knowing a test name

#### Requirements:

1. use Travis CI and codecov 
2. cover at least all public methods/functions
3. have long names based on a pattern ```test_<WHAT1>_on_<WHAT2>_<DOES_WHAT>```:
   - `<WHAT1>` name of function/method name under test, eg `upload`, `upload_method`, `status_property`
   - `<WHAT2>` context/condition or arguments, eg `on_negative_integer`, `on_init`, `on_teardown` 
   - `<DOES_WHAT>` expected result or behaviour, eg `returns_none`, `raises_error` 
   - regrassion tests / bugfixes are named based on behaviour
4. one test addresses one issue and has one assert per test
5. have clear separation of setup, call of code under test and result check 
6. assembled by testcases: one testclass class for every single class in code under test

Learning
--------
Basic testing in python:
- <http://docs.python-guide.org/en/latest/writing/tests/>

Takeaways from <https://pylonsproject.org/community-unit-testing-guidelines.html>:
- tests should be as simple as possible
- tests should be isolated
- each test method should test Just One Thing

Very concise guide: <https://gist.github.com/sloria/7001839#testing>

[Property testing](http://hypothesis.works/articles/what-is-property-based-testing/)

Test naming
-----------

Tests have to be named properly and clearly tell:
- what function or method is tested
- what input or context is given
- what is the expected result or behaviour

```
[the name of the tested method]_[expected input / tested state]_[expected behavior]

[expected behavior] is usually [returns_something | raises_something | ...]
```

#### Examples:

```test_get_method_on_csv_format_arg_returns_expected_string```

1. Name of the method under test: ```get```
2. Expected context: `format` argument equals `csv`
3. Expected behavior: returns string that can be compared to expected value

```test_as_date_on_invalid_string_fails```

1. Name of the method under test: ```as_date```
2. Expected input: string with improper formatting supplied
3. Expected behavior: fails or raises error

#### Comments:
  - smaller tests can have simplier naming, eg ```test_make_date()```
    - regression test (bugfixes) names state the problem, eg ```test_CBR_USD_will_not_work_before_1992```
  
#### Reading:  
  - read about *Arrange-Act-Assert* or *Given-When-Then* for more information
  - [this post](https://stackoverflow.com/questions/155436/unit-test-naming-best-practices) is oftern cited for naming, 
    but discussion has some controversies. 
    
Comments format
---------------

Commenting a test should be done when problems with testing are hard to eliminate during the review. 

The comments help to do proper test naming + separate setup, call and check + have testing suggestions.

#### Example: 

Imagine there is a class ```CalendarHelper``` with ```shift_ahead(days)```.

```
   class Test_CalendarHelper():
   
     def  test_shift_ahead_on_positive_int_returns_date_instance(self):
         # method under test:  shift_ahead(days)
         # context or arguments: positive integer
         # expected result or behaviour:  returns datetime.date instance

         # test setup
         days = 1
         # call
         dt = CalendarHelper.shift_ahead(days)
         # check
         assert isinstance(dt, datetime.date)

         # suggested extensions:
         #    - randomise *days*
         #    - add a test on actual value of method result
         #    - parametrise days-result pairs
         
```


To add 
--------
- testing is not the best technique to ensure code quality (eg reviews - design)

Prior discussions
-----------------
- Flask database testing: <https://github.com/mini-kep/db/issues/10>
- Flask testing: <https://github.com/mini-kep/frontend-app/issues/7>
- parsers testing: <https://github.com/mini-kep/parsers/issues/15>
- earlier on parsers testing: <https://github.com/mini-kep/parser-rosstat-kep/issues/24>
- <https://github.com/epogrebnyak/question-kep-unittest>


Specialised advice 
------------------
I got lots of  professional advice specifically in testing from:
- [Alexey Kryukov](https://www.upwork.com/fl/alexey) 
- [Eduard Bagrov - SYP Agency](https://www.upwork.com/freelancers/~01ce161462df65feaa) 

These people are highly recommended to work with on testing issues. 
