# Stage 1: The Builder Stage
FROM python:3.11-slim AS builder
WORKDIR /app
RUN apt-get update && apt-get install -y gcc

# Copy dependencies and install them
COPY dependencies.txt .
RUN pip install --user -r dependencies.txt

# Stage 2: The Runner (Production Stage)
FROM python:3.11-slim AS runner
WORKDIR /app

# Create a restricted user named appuser
RUN useradd --system --user-group appuser

# Copy installed libraries from the builder stage
COPY --from=builder /root/.local /home/appuser/.local
COPY . .

# Update folder permissions for the restricted user
RUN chown -R appuser:appuser /app

# Log out of root and switch to appuser
USER appuser

# Ensure Python can find the installed packages
ENV PATH=/home/appuser/.local/bin:$PATH

EXPOSE 8080

CMD ["gunicorn", "--bind", "0.0.0.0:8080", "app:app"]

