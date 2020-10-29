FROM centos AS builder
ENV TZ "America/Porto_Velho"
ENV DOTNET_INCREMENTAL=True
ENV DOTNET_RESTORE_DISABLE_PARALLEL=True
RUN rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
RUN yum -y install dotnet-sdk-2.2
RUN yum -y install aspnetcore-runtime-2.2
RUN yum -y install dotnet-runtime-2.2

COPY ca-trust/*.crt /etc/pki/ca-trust/source/anchors/
RUN update-ca-trust extract
