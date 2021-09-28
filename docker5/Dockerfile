# FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base

# WORKDIR /app
# EXPOSE 80
# EXPOSE 443
# FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build

# WORKDIR /src
# COPY "docker5.csproj" .
# RUN dotnet restore "docker5.csproj"
# COPY . .
# RUN dotnet build . -c Release -o /app/build

# # RUN apt-get install curl

# FROM build AS publish
# RUN dotnet publish "docker5.csproj" -c Release -o /app/publish

# FROM base AS final
# WORKDIR /app
# COPY --from=publish /app/publish .
# ENTRYPOINT ["dotnet", "docker5.dll"]

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

ENV ASPNETCORE_URLS=http://+:80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["docker5.csproj", "docker5/"]
RUN dotnet restore "docker5/docker5.csproj"
COPY . .
WORKDIR "/src/docker5"
RUN dotnet build "docker5.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "docker5.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "docker5.dll"]