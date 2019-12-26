FROM mcr.microsoft.com/dotnet/core/runtime:3.0-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["DotNetCoreContainer2/DotNetCoreContainer2.csproj", "DotNetCoreContainer2/"]
RUN dotnet restore "DotNetCoreContainer2/DotNetCoreContainer2.csproj"
COPY . .
WORKDIR "/src/DotNetCoreContainer2"
RUN dotnet build "DotNetCoreContainer2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DotNetCoreContainer2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotNetCoreContainer2.dll"]