{% if cookiecutter.use_python2 == 'n' -%}
FROM python:3.5
{% else %}
FROM python:2.7
{%- endif %}
ENV PYTHONUNBUFFERED 1

# Requirements have to be pulled and installed here, otherwise caching won't work
ADD ./requirements /requirements

RUN pip install -r /requirements/production.txt

RUN groupadd -r django && useradd -r -g django django
ADD . /app
RUN chown -R django /app

ADD ./compose/django/gunicorn.sh /gunicorn.sh
ADD ./compose/django/entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh && chown django /entrypoint.sh
RUN chmod +x /gunicorn.sh && chown django /gunicorn.sh

WORKDIR /app

ENTRYPOINT ["/entrypoint.sh"]
