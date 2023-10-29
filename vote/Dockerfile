FROM python:3.9.18-alpine3.18
WORKDIR /app/vote
COPY . .
RUN pip install -r requirements.txt
EXPOSE 8080
CMD [ "python", "app.py" ]