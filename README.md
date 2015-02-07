##Notes from reading the official doc/Google Hangout

###Notes from the 1st hour:
- In 1.7, django.utils.unittest and syncdb will be removed. <-- Really? Huh.
- Use the library ```json``` instead of ```simplejson```
- ```python manage.py runserver``` is new in 1.7. 
- https://github.com/etianen/django-herokuapp/tree/master/herokuapp/project_template/project_name <-- starter kit for django (thanks for sharing, David H.)
- Also, "best practice" is to organize all "apps" under an "apps" folder? But this requires changing the BASE_DIR in settings.py. For example: 
```
import os, sys
BASE_DIR = os.path.dirname(os.path.dirname(__file__))
APPS_DIR = os.path.join(BASE_DIR, 'apps')
sys.path.insert(0, BASE_DIR)
sys.path.insert(1, APPS_DIR)
```
(Thanks again, David!)
- Also, there's this nifty text editor for developing w/ python and django: https://www.jetbrains.com/pycharm/
- Some Field classes have required arguments. CharField, for example, requires that you give it a max_length.
- ```class Choice(models.Model):
    question = models.ForeignKey(Question)
``` means each Choice is related to a single Question.

###Notes from 2nd hour:
- Migrations are how Django stores changes to your models (and thus your database schema) - they’re just files on disk. 
- python manage.py makemigrations polls
- python manage.py check
- python manage.py migrate
- Wait... should I be using __str__ or __unicode__ with python2?
- I did NOT know that ```Question.objects.get(pk=1)``` was identical to ```Question.objects.get(id=1)```.
- I forgot this after ```import datetime```: ```from django.utils import timezone```
- Helpful: http://stackoverflow.com/questions/2048777/django-tutorial-what-is-choice-set and https://docs.djangoproject.com/en/dev/topics/db/queries/#backwards-related-objects
- TODO: Read about accessing related objects: https://docs.djangoproject.com/en/1.7/ref/models/relations/
- TODO: Read about Field Lookups: https://docs.djangoproject.com/en/1.7/topics/db/queries/#field-lookups-intro
- https://docs.djangoproject.com/en/1.7/topics/auth/#module-django.contrib.auth is the authentication framework shipped by Django.
- This is awesome in admin.py:
```
class QuestionAdmin(admin.ModelAdmin):
	fields = ['pub_date', 'question_text']

admin.site.register(Question,QuestionAdmin)
```
- I DID NOT KNOW THIS:
You can assign arbitrary HTML classes to each fieldset. Django provides a "collapse" class that displays a particular fieldset initially collapsed. 
- Interesting: class ChoiceInline(admin.TabularInline) and class ChoiceInline(admin.StackedInline)
- Oh man, magic search field and free pagination :) -- with search_fields = ['question_text']
- If you can't find your base_site.html from near the end of the tutorial athttps://docs.djangoproject.com/en/1.7/intro/tutorial02/, it's here: https://github.com/django/django/blob/master/django/contrib/admin/templates/admin/base_site.html
- WARNING: Remember to put the /templates folder on the same level as manage.py, and not inside an app.
