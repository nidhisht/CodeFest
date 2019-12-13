# Get base SDK image from microsoft
From mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app

# Copy the CSPROJ and restore any dependencies (Via NUGET)
COPY *.csproj ./
RUN dotnet restore

# Copy the project file and build our release
COPY . ./
RUN dotnet publish -c Release -o out

# Generate runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
EXPOSE 80
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "DockerApi.dll"]