FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
#EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["DemoIdentity.Client/DemoIdentity.Client.csproj", "DemoIdentity.Client/"]
RUN dotnet restore "DemoIdentity.Client/DemoIdentity.Client.csproj"
COPY . .
WORKDIR "/src/DemoIdentity.Client"
RUN dotnet build "DemoIdentity.Client.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DemoIdentity.Client.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DemoIdentity.Client.dll"]