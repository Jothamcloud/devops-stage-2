FROM python:3.10.12-slim
   WORKDIR /app
   COPY pyproject.toml poetry.lock ./
   RUN pip install poetry==1.8.3 && poetry config virtualenvs.create false && poetry install
   COPY . .
   EXPOSE 8000
   CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
