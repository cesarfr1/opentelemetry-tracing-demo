FROM mcr.microsoft.com/dotnet/sdk:8.0-bookworm-slim AS build-env
WORKDIR /app

# Set intermediate stage as build
LABEL stage=app-build

# Copy csproj and restore dependencies
COPY App3.WebApi.csproj ./src/
RUN dotnet restore "./src/App3.WebApi.csproj"

# Copy everything, build and publish
COPY . ./src/
RUN dotnet publish src/*.csproj -c Release -o /app/publish


# Build runtime imagedock
FROM mcr.microsoft.com/dotnet/aspnet:8.0-bookworm-slim
WORKDIR /app
COPY --from=build-env /app/publish .
ENTRYPOINT ["dotnet", "App3.WebApi.dll"]