FROM mcr.microsoft.com/mssql/server:2017-latest

RUN apt-get update && apt-get install -y  \
	curl \
	apt-transport-https

# https://docs.microsoft.com/en-us/sql/connect/odbc/linux/installing-the-microsoft-odbc-driver-for-sql-server-on-linux
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

RUN apt-get install -y locales \
    && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
    && locale-gen

RUN apt-get install -y mssql-tools 

RUN su
RUN echo 'export PATH="$PATH:/opt/mssql/bin"' >> ~/.bashrc
RUN echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
RUN ["/bin/bash", "-c", "source ~/.bashrc"]
RUN /opt/mssql/bin/mssql-conf set sqlagent.enabled true
RUN exit
