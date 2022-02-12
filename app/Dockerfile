FROM python:3.4
LABEL maintainer ArashSar

# set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED 1

# set work directory
WORKDIR /docker_app/app

# install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    postgresql-client \
    libpq-dev \
    gcc \
    && rm -rf /var/lib/apt/lists/*

COPY ./requirements.txt .
RUN pip install -r requirements.txt

# copy project
COPY . .