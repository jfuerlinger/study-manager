FROM mcr.microsoft.com/dotnet/core/aspnet:3.0 AS base
WORKDIR /app
EXPOSE 5000

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /src
COPY ["razor.csproj", "./"]
RUN dotnet restore "razor.csproj"
COPY . .
RUN dotnet build "razor.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "razor.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "razor.dll"]
