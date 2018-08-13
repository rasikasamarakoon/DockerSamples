FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY DockerSample/DockerSample.csproj DockerSample/
RUN dotnet restore DockerSample/DockerSample.csproj
COPY . .
WORKDIR /src/DockerSample
RUN dotnet build DockerSample.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerSample.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerSample.dll"]
