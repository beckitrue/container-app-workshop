FROM python:3.10.0-slim-buster
WORKDIR /flask-simple-app
COPY requirements.txt requirements.txt
COPY app.py app.py
RUN pip3 install -r requirements.txt
CMD ["python3", "-m", "flask", "run", "--host=0.0.0.0"]

