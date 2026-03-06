# syntax=docker/dockerfile:1
FROM python:3.14-slim

# Create non-root user
RUN useradd -m appuser

WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN python -m pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY --chown=appuser:appuser . .

# Switch to non-root user
USER appuser

# Expose the port that the application listens on.
EXPOSE 5000

# Run the application.
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]