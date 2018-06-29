FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR ~GCloudNetCore/TestCoreDocker/
COPY TestCoreDocker.csproj TestCoreDocker/
RUN dotnet restore TestCoreDocker/TestCoreDocker.csproj
COPY . TestCoreDocker/
RUN dotnet build TestCoreDocker/TestCoreDocker.csproj -c Release -o app

FROM build AS publish
RUN dotnet publish TestCoreDocker/TestCoreDocker.csproj -c Release -o app

FROM base AS final
WORKDIR ~GCloudNetCore/TestCoreDocker/app
COPY --from=publish ~GCloudNetCore/TestCoreDocker/app .
ENTRYPOINT ["dotnet", "TestCoreDocker.dll"]
