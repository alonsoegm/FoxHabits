# Use official .NET 8 runtime as base image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["backend-api/backend-api.csproj", "backend-api/"]
RUN dotnet restore "backend-api.csproj"
COPY . .
WORKDIR "/src/backend-api"
RUN dotnet build "backend-api.csproj" -c Release -o /app/build

# Publish stage
FROM build AS publish
RUN dotnet publish "backend-api.csproj" -c Release -o /app/publish

# Final stage
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "backend-api.dll"]
