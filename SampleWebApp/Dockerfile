FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 8081 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["SampleWebApp.csproj", "/"]
RUN dotnet restore "/SampleWebApp.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "SampleWebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SampleWebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SampleWebApp.dll"]