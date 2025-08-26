# Start from your current Python 3.11 image
FROM mcr.microsoft.com/devcontainers/python:3.11

# Avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Install unixODBC runtime, FreeTDS, build tools (required for pymssql)
RUN apt-get update && apt-get install -y \
    unixodbc \
    unixodbc-dev \
    freetds-dev \
    freetds-bin \
    build-essential \
    curl \
    gnupg \
    apt-transport-https

# Install Microsoft ODBC Driver 17 for SQL Server
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get update \
    && ACCEPT_EULA=Y apt-get install -y msodbcsql17

# Set ODBC environment variables
ENV ODBCSYSINI=/etc
ENV ODBCINI=/etc/odbcinst.ini

# Set working directory
WORKDIR /workspaces/RealRoll

# Copy requirements and install Python dependencies
COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Install pymssql separately
RUN pip install --no-cache-dir pymssql
