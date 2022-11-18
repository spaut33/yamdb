FROM python:3.7-slim
WORKDIR /app
COPY requirements.txt .
RUN pip3 install -r /app/requirements.txt --no-cache-dir
COPY . .

CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000"]

LABEL author='roman.petrakov@gmail.com' version=1.1.0 app_name=yamdb
