FROM registry.centos.org/dotnet/dotnet-20-centos7:latest

USER 0

RUN rpm --import "http://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF" && \
#
yum install -y --setopt=tsflags=nodocs install yum-utils && \
yum-config-manager --add-repo http://download.mono-project.com/repo/centos/ && \
yum install -y --setopt=tsflags=nodocs mono-complete && \
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

RUN chown -R 1001:0 /opt/app-root && fix-permissions /opt/app-root

# Run container by default as user with id 1001 (default)
USER 1001

# Set the default CMD to print the usage of the language image.
CMD /usr/libexec/s2i/usage
