# Build Image
FROM mcr.microsoft.com/dotnet/sdk:8.0.201 as build
ARG TARGETPLATFORM
ARG TARGETARCH
RUN echo "I am building for $TARGETPLATFORM and $TARGETARCH"

WORKDIR /source
COPY *.csproj .
RUN dotnet restore

COPY . .
RUN dotnet publish -c release -o /app --self-contained false --no-restore

# Run Image
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Worker.dll"]