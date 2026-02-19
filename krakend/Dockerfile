FROM python:3.11-slim
WORKDIR /app
RUN python -m pip install --no-cache-dir pyyaml
COPY swagger2krakend/app.py /app/app.py
ENTRYPOINT ["python", "/app/app.py"]
CMD ["swagger.yaml", "-o", "krakend.json"]
