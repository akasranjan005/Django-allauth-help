# Django-allauth-help
Cheatsheet to get started with Django-allauth

__author__ = "Akash Ranjan"

# To setup and use django-allauth (Django 1.8)

### You can read about the configurations and all other setups here: http://django-allauth.readthedocs.org/en/latest/installation.html

`sudo pip install django-allauth`

* Go to /usr/local/lib/python2.7/dist-packages/allauth/ and copy the templates folder into your project
* This templates folder can later be modified for customised login/signup page

`configuration for settings.py`
	
	Add:

	AUTHENTICATION_BACKENDS = (
	    # Needed to login by username in Django admin, regardless of `allauth`
	    'django.contrib.auth.backends.ModelBackend',

	    # `allauth` specific authentication methods, such as login by e-mail
	    'allauth.account.auth_backends.AuthenticationBackend',
	)

	TEMPLATES = [
	    {
	        'BACKEND': 'django.template.backends.django.DjangoTemplates',
	        'DIRS': ['your/template/directory/in/your/project'],
	        'APP_DIRS': True,
	        'OPTIONS': {
	            'context_processors': [
	                #other predifined context_processors
	                ...
	                'django.template.context_processors.request',
	                ...
	            ],
	        },
	    },
	]


	INSTALLED_APPS = (
			'allauth',
			'allauth.account',
	 		'allauth.socialaccount',
			'allauth.socialaccount.providers.google',
		)


	#django-allauth configurations
	SITE_ID = 4 #depending upon the site number.. that can be found at localhost:8000/admin/sites/ just hover over your site name
	
	#Theses are the basic configuration that i found useful
	http://django-allauth.readthedocs.org/en/latest/configuration.html

	ACCOUNT_USER_MODEL_USERNAME_FIELD = "username"
	ACCOUNT_EMAIL_REQUIRED = True
	ACCOUNT_USERNAME_REQUIRED = True
	ACCOUNT_AUTHENTICATION_METHOD = 'username'
	ACCOUNT_USERNAME_MIN_LENGTH = 4
	ACCOUNT_EMAIL_VERIFICATION = "mandatory"
	ACCOUNT_EMAIL_CONFIRMATION_EXPIRE_DAYS = 1
	ACCOUNT_LOGIN_ON_EMAIL_CONFIRMATION = True
	ACCOUNT_LOGOUT_ON_GET = True
	ACCOUNT_CONFIRM_EMAIL_ON_GET = True

	SOCIALACCOUNT_QUERY_EMAIL = True
	SOCIALACCOUNT_STORE_TOKENS = True

	LOGIN_REDIRECT_URL = "/"


`For urls.py`

	urlpatterns = [
	    ...
	    url(r'^accounts/', include('allauth.urls')),
	    ...
	]


* Execute the following:
 * `python manage.py migrate`

 * `python manage.py createsuperuser`

 * `python manage.py runserver`


* In browser open http://127.0.0.1:8000/admin/
	
	* Goto http://127.0.0.1:8000/admin/sites/site/ and add a site

* Then some obvious steps like to get client id aand private id from 
	* https://console.developers.google.com/apis

* and put the credentials in django-admin
	* http://127.0.0.1:8000/admin/socialaccount/socialapp/


* For details regarding how to create client id for google authentication
	* https://github.com/googleads/googleads-dotnet-lib/wiki/How-to-create-OAuth2-client-id-and-secret



----------------------------------------------------------------------
## Helpful URLs
----------------------------------------------------------------------
* http://piratelearner.com/en/C/course/computer-science/django/django-all-auth-all-you-need-to-know/8/
* http://django-allauth.readthedocs.org/en/latest/configuration.html


This much will do :)
