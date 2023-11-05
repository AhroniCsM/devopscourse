FROM python:3.8

ENV PYTHONPATH /usr/src/app
WORKDIR /app

COPY consumer.py /app
COPY requirements.txt /app

RUN pip install --no-cache-dir -r /app/requirements.txt

CMD ["python", "consumer.py", "-p", "5672", "-s", "rabbitmq"]