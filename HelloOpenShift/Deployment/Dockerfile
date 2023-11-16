FROM registry.access.redhat.com/ubi8:latest AS build

RUN yum install -y dotnet-sdk-6.0 && \
    yum clean all -y && \
    rm -rf /var/cache/yum/*

WORKDIR /opt/app-root/src
COPY . .
RUN dotnet publish -c Release

FROM registry.access.redhat.com/ubi8:latest

RUN yum install -y dotnet-sdk-6.0 && \
    yum clean all -y && \
    rm -rf /var/cache/yum/*

COPY --from=build /opt/app-root/src/HelloOpenShift/bin /opt/app-root/src/bin
WORKDIR /opt/app-root/src/bin/Release/net6.0/publish

ENV ASPNETCORE_URLS=http://*:8080
EXPOSE 8080

CMD ["dotnet", "HelloOpenShift.dll"]