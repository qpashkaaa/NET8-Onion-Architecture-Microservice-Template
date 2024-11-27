FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /src

COPY . ./
RUN dotnet restore
RUN dotnet build --no-restore -c Release

FROM build AS server-build
WORKDIR /src/$safeprojectname$.Server
RUN dotnet publish -c Release -o /app

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=server-build /app .
EXPOSE 8080
ENTRYPOINT ["dotnet", "$safeprojectname$.Server.dll"]
