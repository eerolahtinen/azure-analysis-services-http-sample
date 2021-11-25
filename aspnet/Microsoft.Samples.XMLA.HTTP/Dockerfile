# https://hub.docker.com/_/microsoft-dotnet
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY *.sln .
COPY Microsoft.Samples.XMLA.HTTP.Proxy/*.csproj ./Microsoft.Samples.XMLA.HTTP.Proxy/
RUN dotnet restore

# copy everything else and build app
COPY Microsoft.Samples.XMLA.HTTP.Proxy/. ./Microsoft.Samples.XMLA.HTTP.Proxy/
WORKDIR /source/Microsoft.Samples.XMLA.HTTP.Proxy
RUN dotnet publish -c release -o /app --no-restore

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app ./
EXPOSE 80
ENTRYPOINT ["dotnet", "aspnetapp.dll"]
