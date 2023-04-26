FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Internet_store/Internet_store.csproj", "Internet_store/"]
RUN dotnet restore "Internet_store/Internet_store.csproj"
COPY . .
WORKDIR "/src/Internet_store"
RUN dotnet build "Internet_store.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Internet_store.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Internet_store.dll"]
