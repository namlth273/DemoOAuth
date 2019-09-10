FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
#EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["DemoIdentity.Server/DemoIdentity.Server.csproj", "DemoIdentity.Server/"]
RUN dotnet restore "DemoIdentity.Server/DemoIdentity.Server.csproj"
COPY . .
WORKDIR "/src/DemoIdentity.Server"
RUN dotnet build "DemoIdentity.Server.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DemoIdentity.Server.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DemoIdentity.Server.dll"]