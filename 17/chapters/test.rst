Automated Testing
=================

It is good practice to get into the habit of writing and developing tests. A lot of software engineering is about writing and developing tests and test suites in order to ensure the software is robust. Of course, most of the time, we are too busy trying to build things to bother about making sure that they work. Or too arrogant to believe it would fail.

According to the `Django Tutorial  <https://docs.djangoproject.com/en/1.7/intro/tutorial05/>`_, there are numerous reasons why you should include tests:

* Test will save you time: a change in a complex system can cause failures in unpredictable places.
* Tests dont just identify problems, they prevent them: tests show where the code is not meeting expectations.
* Test make your code more attractive: "Code without tests is broken by design", Jacob Kaplan-Moss, One of Django's original developers.
* Tests help teams work together: they make sure your team doesn't inadvertently break your code.


Running Tests
-------------

In built in Django is machinery to test the applications built. You can do this by issuing the following command:

..

	$ python manage.py test rango
	
	Creating test database for alias 'default'...

	----------------------------------------------------------------------
	Ran 0 tests in 0.000s

	OK
	Destroying test database for alias 'default'...
	
	
This will run through the tests associated with the rango application. At the moment, nothing much happens. That is because you may have noticed the file ``rango/tests.py`` only contains an import statement. Everytime you create an application, Django automatically creates such a file to encourage you to write tests. 

From this output, you might also notice that a database called ``default`` is referred to. When you run tests, a temporary database is constructed, which your tests can populate, and perform operations on. This way your testing is performed independently of your live database. 



Testing the models in Rango
---------------------------

Ok, lets create a test. In the Category model, we want to ensure that views are either zero or positive, because the number of views, let's say, can never be less than zero. To create a test for this we can put the following code into ``rango/tests.py``:

.. code-block:: python


	from django.test import TestCase

	from rango.models import Category

	class CategoryMethodTests(TestCase):

	    def test_ensure_views_are_positive(self):

	        """
			ensure_views_are_positive should results True for categories where views are zero or positive
	        """
			cat = Category(name='test',views=-1, likes=0)
			cat.save()
			self.assertEqual((cat.views >= 0), True)



The first thing you should notice, if you have not written tests before, is that we have to inherit from TestCase. The naming over the method in the class also follows a convention, all tests start with ``test_`` and they also contain some type of assertion, which is the test. Here we are check if the values are equal, with the ``assertEqual`` method, but other types of assertions are also possible. See the Python Documentation on unit tests, https://docs.python.org/2/library/unittest.html for other commands (i.e. ``assertItemsEqual``, ``assertListEqual``, ``assertDictEqual``, etc). Django's testing machinery is derived from Python's but also provides an number of other asserts and specific test cases.


Now lets run test:


..

	$ python manage.py test rango
	
	
	Creating test database for alias 'default'...
	F
	======================================================================
	FAIL: test_ensure_views_are_positive (rango.tests.CategoryMethodTests)
	----------------------------------------------------------------------
	Traceback (most recent call last):
	  File "/Users/leif/Code/tango_with_django_project_17/rango/tests.py", line 12, in test_ensure_views_are_positive
	    self.assertEqual((cat.views>=0), True)
	AssertionError: False != True

	----------------------------------------------------------------------
	Ran 1 test in 0.001s

	FAILED (failures=1)
	


As we can see this test fails. This is because the model does not check whether the value is less than zero or not. Since we really want to ensure that the values are non-zero, we will need to update the model, to ensure that this requirement is fulfilled. Do this now by adding some code to the Catgegory models, ``save()`` method, that checks the value of views, and updates it accordingly.


#TODO(leifos): add reference to forms chapter. 

Once you have updated your model, you can now re-run the test, and see if your code now passes it. If not, try again.



Let's try adding another test, that ensures an appropriate slug line is created i.e. one with dashes, and in lowercase. Add the following code to ``rango/tests.py``:

.. code-block:: python


	   def test_slug_line_creation(self):
	   		"""
			slug_line_creation checks to make sure that when we add a category an appropriate slug line is created
			i.e. "Random Category String" -> "random-category-string"
			"""

			cat = cat('Random Category String')
			cat.save()
			self.assertEqual(cat.slug, 'random-category-string')


Does your code work?



Testing Views
-------------
#TODO(leifos): Add in examples that test the output of views.
 

Testing the Rendered Page
-------------------------
#TODO(leifos): add an example using either Django's test client and/or Selenium, which is are "in-browser" frameworks to test the way the HTML is rendered in a browser.


Coverage Testing
----------------
Code coverage measures how much of your code base has been tested, and how much of your code has been put through its paces via tests. You can install a package called ``coverage`` via with ``pip install coverage`` which automatically analyses how much code coverage you have. Once you have ``coverage`` installed, run the following command:

..

	$ coverage run --source='.' manage.py test rango
	

This will run through all the tests and collect the coverage data for the rango application. To see the coverage report you need to then type:


..

	$ coverage report
	
	Name                                       Stmts   Miss  Cover
	--------------------------------------------------------------
	manage                                         6      0   100%
	populate                                      33     33     0%
	rango/__init__                                 0      0   100%
	rango/admin                                    7      0   100%
	rango/forms                                   35     35     0%
	rango/migrations/0001_initial                  5      0   100%
	rango/migrations/0002_auto_20141015_1024       5      0   100%
	rango/migrations/0003_category_slug            5      0   100%
	rango/migrations/0004_auto_20141015_1046       5      0   100%
	rango/migrations/0005_userprofile              6      0   100%
	rango/migrations/__init__                      0      0   100%
	rango/models                                  28      3    89%
	rango/tests                                   12      0   100%
	rango/urls                                    12     12     0%
	rango/views                                  110    110     0%
	tango_with_django_project/__init__          0      0   100%
	tango_with_django_project/settings         28      0   100%
	tango_with_django_project/urls              9      9     0%
	tango_with_django_project/wsgi              4      4     0%
	--------------------------------------------------------------
	TOTAL                                        310    206    34%
	


We can see from the above report that critical parts of the code have not been tested, ie. ``rango/views``. For more details about using the package ``coverage`` visit: http://nedbatchelder.com/code/coverage/ 




Exercises
---------
* Add tests the other models. 
* Undertake  `Part Five of the official Django Tutorial  <https://docs.djangoproject.com/en/1.7/intro/tutorial05/>`_ to learn about automated testing.
* Check out the `tutorial on test driven development by Harry Percival <http://www.tdd-django-tutorial.com>`_.

