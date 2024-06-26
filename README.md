# 🐵 django-mailchimp-auth

A reusable application to allow users of your Django application to
"authenticate" against your [Mailchimp](https://mailchimp.com/) user store.

## TODO: Update README to include instructions for reCAPTCHA.

## Pre-requisites

- [jQuery](https://jquery.com/)
- [Bootstrap](https://getbootstrap.com/)

## Quick start

1. Add `mailchimp_auth` to your `INSTALLED_APPS`:

    ```python
    INSTALLED_APPS = [
        ...
        'mailchimp_auth',
    ]
    ```

2. Include the `mailchimp_auth` URLs in your project URL conf:

    ```python
    path('mailchimp/', include('mailchimp_auth.urls')),
    ```

3. Run `python manage.py migrate` to create the `mailchimp_auth` models.

4. Add the following to your project settings, being sure to fill in real
values.


    ```python
    # Configure Django email backend: https://docs.djangoproject.com/en/2.2/topics/email/#smtp-backend
    EMAIL_USE_TLS = True
    EMAIL_HOST = ''  # e.g., smtp.gmail.com
    EMAIL_HOST_USER = ''  # e.g., youremail@email.com
    EMAIL_HOST_PASSWORD = ''
    EMAIL_PORT = 0  # e.g., 587
    DEFAULT_FROM_EMAIL = ''  # e.g., '<testing@datamade.us>'

    # Configure Mailchimp
    # https://mailchimp.com/developer/marketing/guides/quick-start/#make-your-first-api-call
    MAILCHIMP_API_KEY = '<secret key>'
    MAILCHIMP_SERVER = '<server code>'
    MAILCHIMP_LIST_ID = '<id of list to search within>'
    MAILCHIMP_INTEREST_ID = '<comma separated string of interest ids (eg. xxx,yyyy,zzzzz)>'
    MAILCHIMP_TAG = '<string value of a tag to add to users (optional)>'

    # Name and domain for cookie set for authorized users
    MAILCHIMP_AUTH_COOKIE_NAME = ''  # e.g., mailchimp-auth
    MAILCHIMP_AUTH_COOKIE_DOMAIN = ''  # e.g., datamade.us

    # Location to which user will be redirected on authorization
    MAILCHIMP_AUTH_REDIRECT_LOCATION = '/'
    ```

5. Include <a href="https://github.com/keaukraine/bootstrap4-fs-modal">Bootstrap Mobile Fullscreen Modals</a>,
authentication modals, and required JavaScript in templates that require login.

    ```html
    <link href="{% static 'css/bootstrap-fs-modal.css' %}" rel="stylesheet">

    ...

    {% include 'auth_modals.html' %}

    ...

    <script src="{% static 'js/render_mailchimp_auth.js' %}"></script>

    {% if messages %}
    <script type="text/javascript">
      $('#messageModal').modal()
    </script>
    {% endif %}
    ```

6. Trigger the login or signup modal.

    ```html
    $('#loginModal').modal()
    ```


### Sending Sentry messages to an admin email

This app can send authentication error messages to an admin similar to those sent to sentry. If you have a `SENTRY_DSN` in your environment variables, simply add a var named `ADMIN_EMAIL` containing an email address string as well.
