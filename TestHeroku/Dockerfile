FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY TestHeroku/TestHeroku.csproj TestHeroku/
RUN dotnet restore TestHeroku/TestHeroku.csproj
COPY . .
WORKDIR /src/TestHeroku
RUN dotnet build TestHeroku.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish TestHeroku.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
CMD dotnet TestHeroku.dll