FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["UploadService/UploadService.csproj", "UploadService/"]
RUN dotnet restore "UploadService/UploadService.csproj"
COPY . .
WORKDIR "/src/UploadService"
RUN dotnet build "UploadService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "UploadService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "UploadService.dll"]
