FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

 

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Labb1Publisering/Labb1Publisering.csproj", "Labb1Publisering/"]
RUN dotnet restore "Labb1Publisering/Labb1Publisering.csproj"
COPY . .
WORKDIR "/src/Labb1Publisering"
RUN dotnet build "Labb1Publisering.csproj" -c Release -o /app/build

 

FROM build AS publish
RUN dotnet publish "Labb1Publisering.csproj" -c Release -o /app/publish /p:UseAppHost=false

 

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Labb1Publisering.dll"]