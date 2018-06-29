FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY TestCoreDocker/TestCoreDocker.csproj TestCoreDocker/
RUN dotnet restore TestCoreDocker/TestCoreDocker.csproj
COPY . .
WORKDIR /src/TestCoreDocker
RUN dotnet build TestCoreDocker.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish TestCoreDocker.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestCoreDocker.dll"]
