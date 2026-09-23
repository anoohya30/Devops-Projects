FROM ubuntu:latest

RUN apt update && apt install -y python3 python3-setuptools python3-dev build-essential python3-pip
RUN pip3 install flask --break-system-packages
COPY app.py /mnt/app.py
EXPOSE 8080
CMD ["python3", "/mnt/app.py"]


