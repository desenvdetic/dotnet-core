FROM registry.centos.org/dotnet/dotnet-22-runtime-centos7:latest

USER 0

COPY ca-trust/*.crt /etc/pki/ca-trust/source/anchors/
RUN update-ca-trust extract

RUN yum install -y --setopt=tsflags=nodocs install yum-utils && \
rpm --import https://download.mono-project.com/repo/xamarin.gpg  && \
curl https://download.mono-project.com/repo/centos7-stable.repo | tee /etc/yum.repos.d/mono-centos7-stable.repo && \
#
yum install -y --setopt=tsflags=nodocs mono-complete && \
#
ln -s /usr/lib64/libdl.so.2 /usr/lib64/libdl.so && \
#
yum install -y --setopt=tsflags=nodocs fontconfig && \
yum install -y --setopt=tsflags=nodocs freetype && \
yum install -y --setopt=tsflags=nodocs libpng && \
yum install -y --setopt=tsflags=nodocs libjpeg && \
yum install -y --setopt=tsflags=nodocs openssl && \
yum install -y --setopt=tsflags=nodocs icu && \
yum install -y --setopt=tsflags=nodocs libX11 && \
yum install -y --setopt=tsflags=nodocs libXext && \
yum install -y --setopt=tsflags=nodocs libXrender && \
yum install -y --setopt=tsflags=nodocs xorg-x11-fonts-Type1 && \
yum install -y --setopt=tsflags=nodocs xorg-x11-fonts-75dpi && \
rpm -iv https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox-0.12.5-1.centos7.x86_64.rpm  && \
#
mkdir -p  /opt/app-root/app/Rotativa/Linux/  && \
#
ln -s /usr/local/bin/wkhtmltopdf /opt/app-root/app/Rotativa/Linux/wkhtmltopdf  && \
ln -s /usr/local/bin/wkhtmltoimage /opt/app-root/app/Rotativa/Linux/wkhtmltoimage  && \
#
yum clean all -y && \
rm -rf /var/cache/yum/*
#
RUN chown -R 1001:0 /opt/app-root && fix-permissions /opt/app-root
#
# Run container by default as user with id 1001 (default)
USER 1001
#
# Set the default CMD to print the usage of the language image.
CMD /usr/libexec/s2i/usage
