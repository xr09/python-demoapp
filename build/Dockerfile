FROM python:3.12-slim-bookworm

LABEL Name="Python Flask Demo App" Version=1.5.0
LABEL org.opencontainers.image.source = "https://github.com/xr09/python-demoapp"

ARG srcDir=src
WORKDIR /app
COPY $srcDir/requirements.txt .

RUN set -eux; \
    apt update; \
    apt-get install --no-install-recommends -y build-essential; \
    pip install --no-cache-dir -r requirements.txt; \
    apt-get -y purge build-essential; \
    apt-get -y autoremove

COPY $srcDir/run.py .
COPY $srcDir/app ./app

EXPOSE 5000

CMD ["gunicorn", "-b", "0.0.0.0:5000", "run:app"]
