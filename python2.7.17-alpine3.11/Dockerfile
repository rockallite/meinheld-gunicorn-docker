FROM python:2.7.17-alpine3.11

LABEL maintainer="Rockallite Wulf <rockallite.wulf@gmail.com>"

RUN apk add --no-cache --virtual .build-deps gcc libc-dev \
    && pip install meinheld gunicorn \
    && rm -rf ~/.cache/pip \
    && apk del .build-deps

COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

COPY ./start.sh /start.sh
RUN chmod +x /start.sh

COPY ./gunicorn_conf.py /gunicorn_conf.py

COPY ./app /app
WORKDIR /app/

ENV PYTHONPATH=/app

EXPOSE 80

ENTRYPOINT ["/entrypoint.sh"]

# Run the start script, it will check for an /app/prestart.sh script (e.g. for migrations)
# And then will start Gunicorn with Meinheld
CMD ["/start.sh"]
