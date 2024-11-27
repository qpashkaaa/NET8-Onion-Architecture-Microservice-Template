FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /src

COPY . ./
RUN dotnet restore
RUN dotnet build --no-restore -c Release

FROM build AS migrator-build
WORKDIR /src/FactsMicroservice.Migrator
RUN dotnet publish -c Release -o /app

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=migrator-build /app .
EXPOSE 8080
ENTRYPOINT ["dotnet", "FactsMicroservice.Migrator.dll"]
