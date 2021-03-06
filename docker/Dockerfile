FROM python:3.9-slim

# Allow service to handle stops gracefully
STOPSIGNAL SIGQUIT

# Set pip to have cleaner logs and no saved cache
ENV PIP_NO_CACHE_DIR=false \
    PIPENV_HIDE_EMOJIS=1 \
    PIPENV_NOSPIN=1

# Install git
RUN apt-get -y update \
    && apt-get install -y \
        git gcc \
    && rm -rf /var/lib/apt/lists/*

# Create non-root user.
RUN useradd --system --shell /bin/false --uid 1500 challenger

# Install pipenv
RUN pip install -U pipenv

# Copy the project files into working directory
WORKDIR /app
COPY . .

# Install project dependencies
RUN pipenv install --system --deploy

# Run web server through custom manager
ENTRYPOINT ["python", "manage.py"]
CMD ["run"]
