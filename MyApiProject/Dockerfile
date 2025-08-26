# Development Dockerfile for .NET Core API
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["MyApiProject.csproj", "."]
RUN dotnet restore "MyApiProject.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "MyApiProject.csproj" -c Debug -o /app/build

FROM build AS publish
RUN dotnet publish "MyApiProject.csproj" -c Debug -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyApiProject.dll"]
