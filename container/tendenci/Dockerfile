FROM ubuntu:16.04
ARG project_name=tendenciBitWorks
RUN apt-get update; apt-get install -y \
    python-pip \
    build-essential \
    python-dev \
    libevent-dev \
    libpq-dev \
    libjpeg8 \
    libjpeg-dev \
    libfreetype6 \
    libfreetype6-dev \
    libmemcached-dev \
    libproj-dev \
    gdal-bin
RUN pip install tendenci
WORKDIR /var/www/
RUN django-admin startproject --template=https://github.com/tendenci/tendenci-project-template/archive/master.zip ${project_name}
WORKDIR /var/www/${project_name}
COPY local_settings.py conf/local_settings.py
EXPOSE 8000
ENTRYPOINT ["/usr/local/bin/gunicorn"]
CMD ["--bind=0.0.0.0:8000", "conf.wsgi:application"]
