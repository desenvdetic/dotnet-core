FROM centos:8

# INSTALAÇÃO DE AUTORIDADE CERTIFICADORA NO CENTOS
ADD  https://raw.githubusercontent.com/desenvdetic/ca-trust/main/openshift_rootCA.crt \
https://raw.githubusercontent.com/desenvdetic/ca-trust/main/portainer_rootCA.crt /etc/pki/ca-trust/source/anchors/
RUN update-ca-trust extract

# INSTALAÇÃO DO SDK 3.1 DOTNET
RUN dnf install -y --setopt=tsflags=nodocs dotnet-sdk-3.1 aspnetcore-runtime-3.1 && dnf clean all -y

ENV ASPNETCORE_URLS=http://+:80;https://+:443
ENV ASPNETCORE_HTTPS_PORT=443

EXPOSE 80 443