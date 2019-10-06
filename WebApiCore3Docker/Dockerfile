FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["WebApiCore3Docker/WebApiCore3Docker.csproj", "WebApiCore3Docker/"]
RUN dotnet restore "WebApiCore3Docker/WebApiCore3Docker.csproj"
COPY . .
WORKDIR "/src/WebApiCore3Docker"
RUN dotnet build "WebApiCore3Docker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApiCore3Docker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApiCore3Docker.dll"]