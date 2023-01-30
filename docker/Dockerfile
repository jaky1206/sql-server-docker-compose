FROM mcr.microsoft.com/mssql/server:2022-latest

USER root

# Update the list of packages
RUN apt-get update

# Install pre-requisite packages.
# This transport supports server as well as client authentication with certificates. 
RUN apt-get install -y curl apt-transport-https 
# This package contains tools to generate locale definitions from source files (included in this package). 
RUN apt-get install -y locales && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen


# Import the public repository GPG keys.
RUN wget -q "https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb"
# Register the Microsoft repository GPG keys
RUN dpkg -i packages-microsoft-prod.deb
# Update the list of packages
RUN apt-get update


# Install PowerShell
RUN apt-get install -y powershell
# Install missing dependencies
RUN apt-get install -f


RUN echo 'export PATH="$PATH:/opt/mssql/bin"' >> ~/.bashrc
RUN echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
RUN ["/bin/bash", "-c", "source ~/.bashrc"]

RUN /opt/mssql/bin/mssql-conf set sqlagent.enabled true
RUN /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false

USER 1001



