# Use the official .NET Core SDK image as the base image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the project file(s) to the working directory
COPY ./*.csproj ./
# Restore the NuGet packages

# Copy the remaining source code to the working directory
COPY . ./

# Publish the application
RUN dotnet publish -c Release -o out --no-cache
#  no need to add no-restore or adding restore step https://stackoverflow.com/a/73484824


# Use the official .NET Core Runtime image as the base image for the final image
FROM mcr.microsoft.com/dotnet/runtime:8.0

# Set the working directory inside the container
WORKDIR /app

# Copy the published output from the build image to the final image
COPY --from=build /app/out ./

# Set the entry point for the container
ENTRYPOINT ["dotnet", "HelloWorld.dll"]