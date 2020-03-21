FROM centos AS base

ENV TZ "America/Porto_Velho"

RUN rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
RUN yum -y install dotnet-sdk-3.1
RUN yum -y install aspnetcore-runtime-3.1
RUN yum -y install dotnet-runtime-3.1

COPY ca-trust/*.crt /etc/pki/ca-trust/source/anchors/
RUN update-ca-trust extract
