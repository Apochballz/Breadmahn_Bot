# Use official Python image
FROM python:3.11-slim

# Install system dependencies including TA-Lib requirements
RUN apt-get update && apt-get install -y \
    build-essential \
    libta-lib-dev \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy requirements file
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy all Python files
COPY . .

# Command to run the application
# Note: We'll use gunicorn with app.py (Flask wrapper)
CMD ["gunicorn", "--bind", "0.0.0.0:$PORT", "app:app"]