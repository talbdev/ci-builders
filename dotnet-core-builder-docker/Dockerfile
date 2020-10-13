ARG DOCKER_BASE_IMAGE
FROM $DOCKER_BASE_IMAGE
MAINTAINER talbdev <lab>

ARG DOTNET_SDK_VERSION
ARG DOTNET_SDK_BASE_URL
ARG POWERSHELL_VERSION
ARG POWERSHELL_BASE_URL

ENV DOTNET_RUNNING_IN_CONTAINER=true
ENV DOTNET_USE_POLLING_FILE_WATCHER=true
ENV NUGET_XMLDOC_MODE=skip

RUN yum install -y \
        wget \
        git \
        curl \
        nano \
        gcc \
        make \
        libicu \
        libicu-devel.x86_64 \
    && yum -y groupinstall development \
    && yum clean all \
    && rm -rf /var/cache/yum

# Install DOTNET SDK.
RUN curl -SL --output dotnet.tar.gz ${DOTNET_SDK_BASE_URL}/${DOTNET_SDK_VERSION}/dotnet-sdk-${DOTNET_SDK_VERSION}-linux-x64.tar.gz \
    && mkdir -p /usr/share/dotnet \
    && tar -ozxf dotnet.tar.gz -C /usr/share/dotnet \
    && rm -rf dotnet.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
    # Trigger first run experience by running arbitrary cmd
    && dotnet help
    
# Install Powershell
RUN curl -SL --output powershell.tar.gz ${POWERSHELL_BASE_URL}/${POWERSHELL_VERSION}/powershell-${POWERSHELL_VERSION}-linux-x64.tar.gz \
    && mkdir -p /opt/microsoft/powershell/${POWERSHELL_VERSION} \
    && tar -zxf powershell.tar.gz -C /opt/microsoft/powershell/${POWERSHELL_VERSION} \
    && rm -rf powershell.tar.gz \
    && chmod +x /opt/microsoft/powershell/${POWERSHELL_VERSION}/pwsh \
    && ln -s /opt/microsoft/powershell/${POWERSHELL_VERSION}/pwsh /usr/bin/pwsh
    

CMD ["dotnet"]
