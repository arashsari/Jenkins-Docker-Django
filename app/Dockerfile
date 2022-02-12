FROM python:3
LABEL maintainer ArashSar

# set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED 1

# set work directory
WORKDIR /docker_app/app

# install dependencies
RUN apt-get update && apt-get install -y \
    libpq-dev \
    gcc \
    gettext \
    musl-dev

# # install psycopg2 dependencies
# RUN apk update \
#     && apk add postgresql-dev gcc python3-dev musl-dev

# Requirements are installed here to ensure they will be cached.
# COPY ./requirements.txt /docker_app/code/requirements.txt
# RUN pip install --no-cache-dir --default-timeout=200 -r /requirements.txt \
#     && rm -rf /requirements.txt
COPY ./requirements.txt .
RUN pip install -r requirements.txt

# copy project
COPY . .

# COPY ./entrypoint.sh /entrypoint
# RUN sed -i 's/\r$//g' /entrypoint
# RUN chmod +x /entrypoint

# COPY ./start-django.sh /start-django
# RUN sed -i 's/\r$//g' /start-django
# RUN chmod +x /start-django

# COPY . /app

# COPY config/nginx/default /etc/nginx/sites-available/default
# COPY config/nginx/nginx.conf /etc/nginx/nginx.conf

# WORKDIR /app

# EXPOSE 80/tcp 443/tcp

# ENTRYPOINT ["/entrypoint"]

# CMD ["sh" , "/start-django"]