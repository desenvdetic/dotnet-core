FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base

COPY ca-trust/*.crt /usr/local/share/ca-certificates/extra/
RUN update-ca-certificates