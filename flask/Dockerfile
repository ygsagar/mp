# Use a lightweight Python image
FROM python:3.10-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the dependencies file
COPY requirements.txt requirements.txt

# Install dependencies
RUN pip install --upgrade pip && \
    pip install tensorflow-cpu==2.14.0 && \
    pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application
COPY . .

# Expose the port Flask runs on (Google Cloud Run requires port 8080)
EXPOSE 8080

# Command to run the app (change "app" to your file name)
CMD ["gunicorn", "-b", "0.0.0.0:8080", "vulnerability_detection:app"]
