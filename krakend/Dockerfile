FROM python:3.11-slim@sha256:d6e4d224f70f9e0172a06a3a2eba2f768eb146811a349278b38fff3a36463b47
WORKDIR /app
RUN python -m pip install --no-cache-dir pyyaml
COPY swagger2krakend/app.py /app/app.py
ENTRYPOINT ["python", "/app/app.py"]
CMD ["swagger.yaml", "-o", "krakend.json"]
