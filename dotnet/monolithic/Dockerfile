# Base stage for runtime dependencies
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 8080


# Build stage using .NET 8.0 SDK
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src

# Copy and restore project dependencies
COPY ["Weather.API/Weather.API.csproj", "Weather.API/"]
RUN dotnet restore "./Weather.API/Weather.API.csproj"

# Copy entire source and build
COPY . .
WORKDIR "/src/Weather.API"
RUN dotnet build "Weather.API.csproj" -c $BUILD_CONFIGURATION -o /app/build


# Publish stage
FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "Weather.API.csproj" -c ${BUILD_CONFIGURATION} -o /app/publish /p:UseAppHost=false


# Final stage
FROM base AS final
WORKDIR /app

# Create non-root user for security
RUN addgroup --system dotnetapp && adduser --system --ingroup dotnetapp dotnetapp

# Copy published files
COPY --from=publish /app/publish .

# Set correct ownership
RUN chown -R dotnetapp:dotnetapp /app

# Switch to non-root user
USER dotnetapp

# Essential environment variables
ENV ASPNETCORE_ENVIRONMENT=Development \
    ASPNETCORE_URLS="http://+:8080" \
    ASPNETCORE_HTTP_PORTS=8080
   

# Application entry point
ENTRYPOINT ["dotnet", "Weather.API.dll"]