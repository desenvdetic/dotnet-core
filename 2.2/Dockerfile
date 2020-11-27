FROM registry.centos.org/dotnet/dotnet-22-centos7:latest AS builder
#
# Run container with root user.
USER 0
#
ENV TZ "America/Porto_Velho"
ENV DOTNET_NUGET_SOURCES "https://nuget.okd.local/repository/nuget-group/"
#ENV DOTNET_INCREMENTAL=True
#ENV DOTNET_RESTORE_DISABLE_PARALLEL=True
# Instalação de autoridade certificadora local.
COPY ca-trust/*.crt /etc/pki/ca-trust/source/anchors/
#
# Instalação dependencias comuns .Net-Core
RUN yum -y update && yum install -y yum-utils
RUN update-ca-trust extract && rpm -i https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
#RUN yum install -y --setopt=tsflags=nodocs
RUN rpmkeys --import "http://pool.sks-keyservers.net/pks/lookup?op=get&search=0x3fa7e0328081bff6a14da29aa6a19b38d3d831ef"
RUN su -c 'curl https://download.mono-project.com/repo/centos7-stable.repo | tee /etc/yum.repos.d/mono-centos7-stable.repo'
RUN yum install -y mono-complete
#
# Instalçao dependencias wkhtmltopdf.
RUN yum install -y \
  wget \
  fontconfig \
  freetype \
  libpng \
  libjpeg \
  openssl \
  icu \
  libX11 \
  libXext \
  libXrender \
  xorg-x11-fonts-Type1 \
  xorg-x11-fonts-75dpi \
  xorg-x11-fonts-100dpi && \
  #
  wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox-0.12.6-1.centos7.x86_64.rpm && \
  rpm -Uvh wkhtmltox-0.12.6-1.centos7.x86_64.rpm && \
  ##
  rpm -i http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
  yum install -y --setopt=tsflags=nodocs --enablerepo=epel \
  cabextract \
  curl \
  fontconfig \
  xorg-x11-font-utils && \
  rpm -i https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm && \
  ##
  mkdir -p /opt/app-root/app/Rotativa/Linux/ && \
  #
  ln -s /usr/local/bin/wkhtmltopdf /opt/app-root/app/Rotativa/Linux/wkhtmltopdf  && \
  ln -s /usr/local/bin/wkhtmltoimage /opt/app-root/app/Rotativa/Linux/wkhtmltoimage  && \
  #
  # Dependencias para qrCode.
  ln -s /usr/lib64/libdl.so.2 /usr/lib64/libdl.so && \
  #
  #Instalação do pacotes para visualização e escrita de imagens
  yum install -y whatprovides libgdiplus libc6 libc6-dev glibc glibc-devel \
  # Limpeza de arquivos temporarios.
  yum clean all -y && \
  rm -rf /var/cache/yum/* && \
  #
  chown -R 1001:0 /opt/app-root && fix-permissions /opt/app-root
#
# Run container by default as user with id 1001 (default)
USER 1001
#
# Set the default CMD to print the usage of the language image.
CMD /usr/libexec/s2i/usage
