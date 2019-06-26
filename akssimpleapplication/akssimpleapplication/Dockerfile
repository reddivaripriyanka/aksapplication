FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["akssimpleapplication/akssimpleapplication.csproj", "akssimpleapplication/"]
RUN dotnet restore "akssimpleapplication/akssimpleapplication.csproj"
COPY . .
WORKDIR "/src/akssimpleapplication"
RUN dotnet build "akssimpleapplication.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "akssimpleapplication.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "akssimpleapplication.dll"]