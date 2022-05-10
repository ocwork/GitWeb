FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["GitWebApp/GitWebApp.csproj", "GitWebApp/"]
RUN dotnet restore "GitWebApp/GitWebApp.csproj"
COPY . .
WORKDIR "/src/GitWebApp"
RUN dotnet build "GitWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "GitWebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GitWebApp.dll"]