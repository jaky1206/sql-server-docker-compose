FROM mcr.microsoft.com/mssql/server:latest

USER root

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

# run the entrypoint script
CMD /opt/mssql/bin/sqlservr

