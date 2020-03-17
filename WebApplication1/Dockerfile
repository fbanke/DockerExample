FROM microsoft/dotnet:2.1.5-aspnetcore-runtime AS base
WORKDIR /src
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
COPY WebApplication1.csproj .

RUN dotnet restore WebApplication1.csproj

WORKDIR /src
COPY . .

RUN dotnet build WebApplication1.csproj -c Release -o app

FROM build AS publish

RUN dotnet publish WebApplication1.csproj -c Release -o /src/app

FROM base AS final
WORKDIR /src
COPY --from=publish /src/app .

ENTRYPOINT ["dotnet", "WebApplication1.dll"]
