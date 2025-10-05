FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Tạo project mới
RUN dotnet new web -n MyApp

# Build và publish từ thư mục MyApp
WORKDIR /src/MyApp
RUN dotnet publish -c Release -o /app/publish

# Stage runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .
EXPOSE 8080
ENTRYPOINT ["dotnet", "MyApp.dll"]
