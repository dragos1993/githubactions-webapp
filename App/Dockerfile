# Use the official Python image from DockerHub
FROM python:3.9-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the current directory's content into the container
COPY . .

# Install Flask (required to run the app)
RUN pip install flask

# Command to run the application
CMD ["python", "app.py"]