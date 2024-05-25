FROM python:3.10-bullseye


WORKDIR /app


COPY . /app


COPY requirements.lock /app/


RUN pip install -r requirements.lock


CMD ["uvicorn", "spaceship.main:app", "--host=0.0.0.0", "--port=8080"]
