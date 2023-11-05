FROM python:3-alpine
ENV PYTHONPATH /usr/src/app
WORKDIR /app
ADD producer.py /app
ADD requirements.txt /app
RUN pip install --upgrade pip
RUN pip install --requirement /app/requirements.txt
