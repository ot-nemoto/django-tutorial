FROM mcr.microsoft.com/devcontainers/python:1-3.12-bullseye

RUN apt update && apt install -y default-mysql-client

ADD requirements.txt .

RUN pip install -r requirements.txt