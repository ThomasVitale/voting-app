# Build Image
FROM mcr.microsoft.com/dotnet/sdk:8.0.201 as build
ARG TARGETPLATFORM
ARG TARGETARCH
RUN echo "I am building for $TARGETPLATFORM"

WORKDIR /source
COPY *.csproj .
RUN dotnet restore -a $TARGETARCH

COPY . .
RUN dotnet publish -c release -o /app -a $TARGETARCH --self-contained false --no-restore

# Run Image
FROM mcr.microsoft.com/dotnet/aspnet:8.0.2
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Worker.dll"]