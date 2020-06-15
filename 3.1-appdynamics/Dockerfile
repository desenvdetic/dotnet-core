FROM registry.centos.org/dotnet/dotnet-31-centos7:latest
#
# Run container with root user.
USER 0
#
ENV TZ "America/Porto_Velho"
# Instalação de autoridade certificadora local.
COPY ca-trust/*.crt /etc/pki/ca-trust/source/anchors/
# RUN update-ca-trust extract
#
# Instalação dependencias comuns .Net-Core
# RUN yum install -y --setopt=tsflags=nodocs install yum-utils && \
RUN \
    update-ca-trust extract && \
    # cp -r ../ca-trust/*.crt /etc/pki/ca-trust/source/anchors/ && update-ca-trust extract && \
    #rpm --import https://download.mono-project.com/repo/xamarin.gpg  && \
    #curl https://download.mono-project.com/repo/centos7-stable.repo | tee /etc/yum.repos.d/mono-centos7-stable.repo && \
    #
    yum install -y --setopt=tsflags=nodocs \
    #mono-complete \
    #
    # Instalçao dependencias wkhtmltopdf.
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
    rpm -i https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox-0.12.5-1.centos7.x86_64.rpm  && \
    ##
    rpm -i http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    yum install -y --setopt=tsflags=nodocs --enablerepo=epel \
    cabextract \
    curl \
    fontconfig \
    xorg-x11-font-utils && \
    rpm -i https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm && \
    ##
    mkdir -p  /opt/app-root/app/Rotativa/Linux/  && \
    #
    ln -s /usr/local/bin/wkhtmltopdf /opt/app-root/app/Rotativa/Linux/wkhtmltopdf  && \
    ln -s /usr/local/bin/wkhtmltoimage /opt/app-root/app/Rotativa/Linux/wkhtmltoimage  && \
    #
    # Dependencias para qrCode.
    ln -s /usr/lib64/libdl.so.2 /usr/lib64/libdl.so && \
    #
    #########
## AppDynamics
RUN mkdir -p /opt/appdynamics/dotnet
ADD libappdprofiler.so /opt/appdynamics/dotnet/
ADD AppDynamics.Agent.netstandard.dll /opt/appdynamics/dotnet/

# Mandatory settings required to attach the agent to the .NET application
ENV CORECLR_PROFILER={57e1aa68-2229-41aa-9931-a6e93bbc64d8} \
    CORECLR_ENABLE_PROFILING=1 \
    CORECLR_PROFILER_PATH=/opt/appdynamics/dotnet/libappdprofiler.so

# Configure connection to the controller
ENV APPDYNAMICS_CONTROLLER_HOST_NAME=172.16.0.15
ENV APPDYNAMICS_CONTROLLER_PORT=8090
ENV APPDYNAMICS_CONTROLLER_SSL_ENABLED=false
ENV APPDYNAMICS_AGENT_ACCOUNT_NAME=customer1
ENV APPDYNAMICS_AGENT_ACCOUNT_ACCESS_KEY=421df19b-1d42-4978-a596-308c0b9749ff

# Configure application identity in AppDynamics
ENV APPDYNAMICS_AGENT_APPLICATION_NAME="Sif"
ENV APPDYNAMICS_AGENT_TIER_NAME="Front-end"
ENV APPDYNAMICS_AGENT_REUSE_NODE_NAME=true
ENV APPDYNAMICS_AGENT_REUSE_NODE_NAME_PREFIX="pod"

# It is possible to configure .NET agent using AppDynamicsConfig.json configuration file instead of environment variables
# ADD AppDynamicsConfig.json /opt/appdynamics/dotnet/
#########
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
