#The Dockerfile starts with the official Python 3.9 image
FROM python:3.9

#exposes port 8080 to make the container accessible on that port.
EXPOSE 8080

#The USER root directive specifies that the container will run as the root user.
USER root

#This sets an environment variable INSTANA_SERVICE_NAME to "payment", 
#which can be used within the container 
ENV INSTANA_SERVICE_NAME=payment

#Sets the working directory to /app,
WORKDIR /app

#Copies the requirements.txt file into the container.
COPY requirements.txt /app/

#installs the Python dependencies listed in the requirements.txt file.
RUN pip install -r requirements.txt

#opy Python files (*.py) and the 
#configuration file (payment.ini) into the /app directory in the container.
COPY *.py /app/
COPY payment.ini /app/

#CMD ["python", "payment.py"]
#UWSGI is robust application server used to serve Python web applications
CMD ["uwsgi", "--ini", "payment.ini"]

