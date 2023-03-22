FROM python:3.7-alpine
COPY . /app
WORKDIR /app
RUN pip install flask flask_cors
EXPOSE 5001
RUN addgroup -S -g 1000 python-app
RUN adduser -S -u 1000 -G python-app python-app
USER 1000
CMD ["python", "app.py"]
