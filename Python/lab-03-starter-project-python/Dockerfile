FROM python:3.10-buster


WORKDIR /app


COPY requirements.lock /app/


RUN pip install -r requirements.lock


COPY . /app


CMD ["uvicorn", "spaceship.main:app", "--host=0.0.0.0", "--port=8080"]