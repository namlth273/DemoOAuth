FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
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