# Base image
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

# Build image
FROM base AS build
WORKDIR /src
COPY . .
RUN dotnet restore DIG_API.csproj
RUN dotnet build DIG_API.csproj -c Release -o /app/build

# Publish image
FROM build AS publish
RUN dotnet publish DIG_API.csproj -c Release -o /app/publish

# Final image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DIG_API.dll"]
