FROM python:3.14-slim@sha256:6a27522252aef8432841f224d9baaa6e9fce07b07584154fa0b9a96603af7456
WORKDIR /app
RUN python -m pip install --no-cache-dir pyyaml
COPY swagger2krakend/app.py /app/app.py
ENTRYPOINT ["python", "/app/app.py"]
CMD ["swagger.yaml", "-o", "krakend.json"]
