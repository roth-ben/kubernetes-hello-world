# Using official python runtime base image
FROM python:3.11-slim

# add curl for healthcheck
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Set the application directory
WORKDIR /app

# Install our requirements.txt
COPY requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt

# Copy our code from the current folder to /app inside the container
COPY . .

# Make port 3001 available for links and/or publish
EXPOSE 3001

# Define our command to be run when launching the container
CMD ["gunicorn", "app:app", "-b", "0.0.0.0:3001", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]
