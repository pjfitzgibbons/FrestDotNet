FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["FrestFSharp/FrestFSharp.fsproj", "FrestFSharp/"]
RUN dotnet restore "FrestFSharp/FrestFSharp.fsproj"
COPY . .
WORKDIR "/src/FrestFSharp"
RUN dotnet build "FrestFSharp.fsproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FrestFSharp.fsproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FrestFSharp.dll"]
