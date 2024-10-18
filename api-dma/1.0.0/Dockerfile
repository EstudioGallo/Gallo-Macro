FROM ghcr.io/estudiogallo/net-core:0.1 AS build

WORKDIR /app
COPY . .
RUN dotnet restore

WORKDIR "/app/src/WebApi"
RUN dotnet build "ApiDma.csproj" -c Release -o /app/out

FROM build AS publish
RUN dotnet publish "ApiDma.csproj" -c Release -o /app/out

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
EXPOSE 8080
ARG ASPNETCORE_ENVIRONMENT=Development
ENV ASPNETCORE_ENVIRONMENT=${ASPNETCORE_ENVIRONMENT}
ENV ASPNETCORE_URLS=http://*:8080
COPY --from=publish /app/out .
ENTRYPOINT ["dotnet", "ApiDma.dll"]
