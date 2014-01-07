General Comments
----------------
- @Siecje thinks we should start using render() rather than render_to_response() at some point.
	- He feels it is important to discuss that there's a shorthand way of getting a response to the client.
	- But I (David) argue it could be confusing - and anyway, render_to_response() drills the concept of context dictionaries into a reader's head.
	- Hmm... I can add a note at some point to discuss this briefly!

EBook and Cover Design
----------------------
- Update sphinx style to compile nicely into ebook
- Get a funky looking coverdesign
- Create a free downloadable ebook and pdf of Tango with Django



Chapter 1
---------
	- fix erd diagram

Chapter 2
---------
- setup Ubuntu 13.4 and try work through and replicate his problems ( pointed out by Mike Gleen
).
- pythonbrew is now deprecated, consider pyenv for linux python installation (@k4rtik)
	

Chapter 4
---------
- add some notes about the use of python manage.py collectstatic, perhaps this would be better in the deployment chapter. (@TMurhpyMusic)


Chapter 5
---------

- by @ramdog and @jonathan-s - should we look at an additional chapter at the end (or section) detailing how to setup up Postgres instead of SQLite? It shouldn't take very long...
- by @jonathan-s - look at South for database handling? Or is this out of scope?

Chapter 7
---------

- Courtesy of Can Obanoglu - In 7.2.1, we start a paragraph with "Besides the CharField and IntegerField widget, many more are available for use." It would be a good idea to add some more fields to our models that use something OTHER than the trivial IntegerField. So maybe we could add a DatePicker or something to specify when an instance was created or something? A good idea!

Chapter 11
---------

- Update to the latest Bootstrap (3.0.2) version as Bootstrap 2.3.2 is no longer officially supported

- Add a note to discuss the problem of forgetting to add a slash to the end of a URL.

Deployment Chapter
------------------
- add list of packages to be installed other than Django and pil

Courtesy of pywebdesign
- What about refactoring to use class-based views?
- Adding a chapter to show how django-allauth could be used to integrate signups.

CLASS-BASED VIEWS (@pywebdesign)
................................
Function based views are very useful and adequate for many other uses which means that an optimal tutorial should cover them too. I find myself looking at your code in views.py and trying to think of a solution to teach class based views without eclipsing function based view! Here's my shortly tough solution:

Make an optional chapter where you teach to convert some views to class based one? This seams to be great and can also allow you to discuss the topic of class based VS function based views. Maybe you will run in some compatibility problem tough, if someone can't follow the tutorial after doing this conversion. The optional chapter should then be made to be read at the end.

With this, your tutorial could become a cornerstone to learning django, I think.

about allauth: here's 2 interesting tutorial:
http://www.sarahhagstrom.com/2013/09/the-missing-django-allauth-tutorial/
https://speakerdeck.com/tedtieken/signing-up-and-signing-in-users-in-django-with-django-allauth



Advanced ORM Chapter
--------------------
- Add a chapter on how to use the object relational mapping in Django.(@kracetheking @k4rtik)





