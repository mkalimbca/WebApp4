#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["WebApp4/WebApp4.csproj", "WebApp4/"]
RUN dotnet restore "WebApp4/WebApp4.csproj"
COPY . .
WORKDIR "/src/WebApp4"
RUN dotnet build "WebApp4.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApp4.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApp4.dll"]