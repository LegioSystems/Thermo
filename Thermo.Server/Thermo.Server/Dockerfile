FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Thermo.Server/Thermo.Server.csproj", "Thermo.Server/"]
RUN dotnet restore "Thermo.Server/Thermo.Server.csproj"
COPY . .
WORKDIR "/src/Thermo.Server"
RUN dotnet build "Thermo.Server.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Thermo.Server.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Thermo.Server.dll"]
