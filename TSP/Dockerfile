FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app
COPY *.csv .

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["TSP.csproj", "TSP/"]
RUN dotnet restore "TSP/TSP.csproj"
COPY . "TSP/"
WORKDIR "/src/TSP"
RUN dotnet build "TSP.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TSP.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TSP.dll"]