FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Shopping.Client.csproj", "."]
RUN dotnet restore "./Shopping.Client.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Shopping.Client.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Shopping.Client.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
# Set the entry point for the application
ENTRYPOINT ["dotnet", "Shopping.Client.dll"]
