# Use the official .NET SDK image for building the application
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
ENV http_proxy http://proxy-chain.intel.com:911
ENV https_proxy http://proxy-chain.intel.com:912
ENV no_proxy intel.com,.intel.com,localhost,127.0.0.1,0.0.0.0

# Set working directory
WORKDIR /app

# Copy project files
COPY *.csproj .
RUN dotnet restore

# Copy the rest of the application code
COPY . .

# Build the application
RUN dotnet publish -c Release -o out

# Use the runtime image for deployment
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY --from=build /app/out .

# Expose the application port
EXPOSE 80
EXPOSE 443

# Start the application
ENTRYPOINT ["dotnet", "AzureAdSample.dll"]
