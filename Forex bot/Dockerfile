# Use official Python image
FROM python:3.11-slim

# Install system dependencies and build TA-Lib FROM SOURCE
RUN apt-get update && apt-get install -y \
    build-essential \
    wget \
    && wget http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz \
    && tar -xzf ta-lib-0.4.0-src.tar.gz \
    && cd ta-lib/ \
    && ./configure --prefix=/usr \
    && make \
    && make install \
    && cd .. \
    && rm -rf ta-lib*

# Set working directory
WORKDIR /app

# Copy requirements file
COPY requirements.txt .

# Install Python dependencies (this will now find the system TA-Lib)
RUN pip install --no-cache-dir -r requirements.txt

# Copy all Python files
COPY . .

# Command to run the application
# Note: We'll use gunicorn with app.py (Flask wrapper)
# Make the script executable and run it
RUN chmod +x start.sh
CMD ["./start.sh"]
