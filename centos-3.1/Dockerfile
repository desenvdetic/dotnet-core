FROM centos:8

# INSTALAÇÃO DE AUTORIDADE CERTIFICADORA NO CENTOS
ADD https://raw.githubusercontent.com/desenvdetic/ca-trust/main/rootCA.crt /etc/pki/ca-trust/source/anchors/
RUN update-ca-trust extract

# INSTALAÇÃO DO SDK 3.1 DOTNET
RUN dnf install -y --setopt=tsflags=nodocs dotnet-sdk-3.1 aspnetcore-runtime-3.1 \
	&& dnf clean all \
	&& rm -rf /var/cache/yum

ENV TZ "America/Porto_Velho"
ENV DOTNET_NUGET_SOURCES "https://nuget.okd.local/repository/nuget-group/"
ENV DOTNET_RESTORE_SOURCES "https://nuget.okd.local/repository/nuget-group/"
ENV DOTNET_INCREMENTAL=True
ENV DOTNET_RESTORE_DISABLE_PARALLEL=True
ENV DOTNET_VERBOSITY=n
#ENV ASPNETCORE_URLS=http://+:80;https://+:443
#ENV ASPNETCORE_HTTPS_PORT=443

#EXPOSE 80 443
