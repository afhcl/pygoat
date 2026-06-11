FROM python:3.9-slim

WORKDIR /app

# Copy requirements first to leverage Docker cache
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application
COPY . .
RUN groupadd --gid 10001 appgroup && useradd --uid 10001 --gid 10001 --system --create-home --shell /usr/sbin/nologin appuser && chown -R appuser:appgroup /app

# Set environment variables
ENV FLASK_APP=app.py
ENV FLASK_ENV=development
ENV PYTHONUNBUFFERED=1

# Expose port 5000
EXPOSE 5000
USER appuser

# Run the application
CMD ["python", "app.py"] 
