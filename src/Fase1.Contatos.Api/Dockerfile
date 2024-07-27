FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["src/Fase1.Contatos.Api/Fase1.Contatos.Api.csproj", "src/Fase1.Contatos.Api/"]
RUN dotnet restore "src/Fase1.Contatos.Api/Fase1.Contatos.Api.csproj"
COPY . .
WORKDIR "/src/src/Fase1.Contatos.Api"
RUN dotnet build "Fase1.Contatos.Api.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "Fase1.Contatos.Api.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Fase1.Contatos.Api.dll"]
