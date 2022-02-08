FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["grpc-service/grpc-service.csproj", "grpc-service/"]
RUN dotnet restore "grpc-service/grpc-service.csproj"
COPY . .
WORKDIR "/src/grpc-service"
RUN dotnet build "grpc-service.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "grpc-service.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "grpc-service.dll"]
