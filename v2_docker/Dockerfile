# Use Python 3.10.11 as the base image
FROM python:3.10.11

# Set the working directory early to maintain consistency
WORKDIR /app

# Upgrade pip and install dependencies in one layer for efficiency
COPY requirements.txt . 
RUN pip install --no-cache-dir --upgrade pip && \
    python -m pip install --no-cache-dir -r requirements.txt

# Set environment variables to optimize Python behavior
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Copy the application code into the container
COPY . /app

# Create a non-root user and set permissions for /app folder
RUN adduser --uid 5678 --disabled-password --gecos "" appuser && \
    chown -R appuser:appuser /app

# Switch to the non-root user for better security
USER appuser

# Default command to run the application
CMD ["python", "baseline_fast_v2.py"]