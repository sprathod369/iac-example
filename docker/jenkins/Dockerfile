FROM jenkins/jenkins:2.282-alpine
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false
COPY default-user.groovy /usr/share/jenkins/ref/init.groovy.d/
COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/plugins.txt
USER root
RUN apk update

# Packages for codescene
RUN apk add jq

# Packages for hg2git migration
RUN apk add mercurial=5.4-r0 git-fast-import=2.26.3-r0

# Packages for ansible, python etc
RUN apk add g++ unixodbc-dev python3-dev py3-pip
RUN pip install --upgrade pip
RUN apk add ansible


# Packages for datahub integration
RUN curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.6.1.1-1_amd64.apk
RUN curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/mssql-tools_17.6.1.1-1_amd64.apk
RUN apk add --allow-untrusted msodbcsql17_17.6.1.1-1_amd64.apk
RUN apk add --allow-untrusted mssql-tools_17.6.1.1-1_amd64.apk