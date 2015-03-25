title: "Django tutorial for python-social-auth"
date: 2015-03-25 15:47:22
comments: false
tags:
- django
- programming
---

I recently had to set up Twitter and Google authentication for a django project I worked on and found the documentation to be a bit lacking for [Python Social Auth][1], so I thought I would document a quick set up here for anyone who is interested. We will need all of the following settings:

{% codeblock lang:python %}
#Step 2
INSTALLED_APPS = (
  ...
  'social.apps.django_app.default',
)

TEMPLATE_CONTEXT_PROCESSORS = (
  ...
  'social.apps.django_app.context_processors.backends',
  'social.apps.django_app.context_processors.login_redirect',
 )

# see step 2 for more info
AUTHENTICATION_BACKENDS = (
  #'social.backends.open_id.OpenIdAuth',
  #'social.backends.google.GoogleOpenId',
  'social.backends.google.GoogleOAuth2',
  #'social.backends.google.GoogleOAuth',
  'social.backends.twitter.TwitterOAuth',
  #'social.backends.yahoo.YahooOpenId',
  'django.contrib.auth.backends.ModelBackend',
)

#Step 3
SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = ""
SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = ""

#step 4
SOCIAL_AUTH_TWITTER_SECRET = ""
SOCIAL_AUTH_TWITTER_KEY = ""
{% endcodeblock %}

1) `pip install python-social-auth` or what ever you prefer

2) Add all of the settings above and run `python manage.py syncdb` to set up the appropriate tables. I will only be talking about twitter and google, but there are dozens of other options [as seen in the docs][1] or on the [projects github page][2].

3) Create a pair of Google OAuth keys:

* Log into the google developer console here: [https://console.developers.google.com/project][3]

* Create project, then click on project name.

* Under APIs & AUTH, select APIs and enable the Google+ API

* Under APIs & AUTH, click "Create new Client ID"

* Select "Web application". If my domain is example.com I will enter in the following:

{% codeblock %}
AUTHORIZED JAVASCRIPT ORIGINS
http://example.com

AUTHORIZED REDIRECT URI
http://example.com/complete/google-oauth2/
{% endcodeblock %}

* I had no trouble with the above, but everything I read online said the above was the most tricky step. Verify the protocol (http vs https) domain, subdomain, port (none above, but my dev server is :8013) and trailing slashes.

* Now You have keys! SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET is your "CLIENT SECRET" on the Googly Plus and SOCIAL_AUTH_GOOGLE_OAUTH2_KEY is your "CLIENT ID"

4) Create a pair of Twitter keys:

* I found twitter super easy, but for completion sake...

* Go to [https://apps.twitter.com/app/new][4] and fill in the forms. I used my raw domain (http://example.com) as my callback url and twitter did not seem to care.

* Go to the API Keys tab

* Put the key and the Secret in the corresponding settings fields as seen above.

5) Add the links to your header template. My full login section looks like this now:

{% codeblock lang:html %}
{% raw %}
    <li>
      <a href="{% url 'login' %}">
        <i class="fa fa-user"></i> Login with Username
      </a>
    </li>
    <li>
      <a href="{% url 'social:begin' 'google-oauth2' %}">
        <i class="fa fa-user"></i> Login with Google+
      </a>
    </li>
    <li>
      <a href="{% url 'social:begin' 'twitter' %}">
        <i class="fa fa-user"></i> Login with Twitter
      </a>
    </li>
{% endraw %}
{% endcodeblock %}

[1]: http://psa.matiasaguirre.net/docs/index.html
[2]: https://github.com/omab/python-social-auth
[3]: https://console.developers.google.com/project
[4]: https://apps.twitter.com/app/new
