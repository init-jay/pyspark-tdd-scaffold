FROM mcr.microsoft.com/devcontainers/python:3.12-bullseye

RUN curl -fsSL https://raw.githubusercontent.com/databricks/setup-cli/main/install.sh | sh

# TODO: obtain client CA for inspection
# COPY ./client_CA.pem /usr/local/share/ca-certificates/client_CA.crt
# RUN chmod 644 /usr/local/share/ca-certificates/client_CA.crt

# ENV REQUESTS_CA_BUNDLE=/usr/local/share/ca-certificates/client_CA.crt
# ENV CA_BUNDLE=/usr/local/share/ca-certificates/client_CA.crt
# ENV SSL_CERT_FILE=/usr/local/share/ca-certificates/client_CA.crt
# ENV NODE_EXTRA_CA_CERTS=/usr/local/share/ca-certificates/client_CA.crt

# RUN update-ca-certificates
# RUN pip3 config set global.cert /usr/local/share/ca-certificates/client_CA.crt