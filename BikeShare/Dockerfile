FROM python:3.11-slim

RUN pip install virtualenv
ENV VIRTUAL_ENV=/venv
RUN virtualenv venv -p python3
ENV PATH="VIRTUAL_ENV/bin:$PATH"

WORKDIR /app
ADD . /app

# Install dependencies
RUN pip install -r requirement.txt

# Expose port
ENV PORT 8080

# Run the application:
# gunicorn and app.py/config.py are not part of this project; run the Flask app directly (it reads $PORT)
CMD ["python", "BikePred.py"]