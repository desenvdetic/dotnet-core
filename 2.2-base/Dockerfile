FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base

COPY ca-trust/*.crt /usr/local/share/ca-certificates/extra/
RUN update-ca-certificates