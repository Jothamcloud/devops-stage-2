FROM python:3.10.12-slim

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file into the container
COPY pyproject.toml poetry.lock ./

# Install Poetry with retry logic
RUN pip install --upgrade pip && \
    pip config set global.timeout 100 && \
    pip install poetry --retries 5 --timeout 100

# Install dependencies
RUN poetry install

# Copy the rest of the application code
COPY . .

# Make port 8000 available to the world outside this container
EXPOSE 8000

# Run the application
CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
