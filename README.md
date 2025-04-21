# Mock Web API

This repo contains basic mock web APIs for purposes such as simulating HTTP 429 conditions with a minimal footprint. It is intended to be a set of APIs that can be used in integrations to make actual API calls but without any storage (or consequence).
The repo is .NET 9 based and uses minimal APIs (see `Program.cs`).

## Developing

### Prerequisities

- [.NET 9 SDK](https://dotnet.microsoft.com/download)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- Switch to the directory into which you cloned the repo.

### Building & Running Locally

#### Build the Project

- Execute `dotnet build .\MockWebAPI\MockWebAPI.csproj` to verify the build works.

#### HTTP-only

- Execute `dotnet run --project .\MockWebAPI\MockWebAPI.csproj` to run. the Kestrel server with http only.
- Issue a curl to get a `Hello World!` response: `curl -v http://localhost:20080`

#### HTTPS/HTTP

- Ensure that you trust the dev certificate: `dotnet dev-certs https --trust`
- Execute `dotnet run --project .\MockWebAPI\MockWebAPI.csproj --launch-profile https` to run the Kestrel server with http and https
- Issue a curl to get a `Hello World!` response: `curl -v http://localhost:20080`
- Issue a curl to get a secure `Hello World!` response: `curl -v https://localhost:20443`

### Building & Running as a Local Container

#### Build the Container

- Start the Docker daemon.
- Execute `docker build -t mockwebapi:1 -f .\MockWebAPI\Dockerfile .\MockWebAPI`

#### HTTP

The container runs under http because the container host where it may run conventionally terminates the secure connection.

- Execute `docker run -p 21080:8080 -t mockwebapi:1` to run. Note the different port to ensure we don't cross streams.
- Issue a curl to get a `Hello World!` response: `curl -v http://localhost:21080`
