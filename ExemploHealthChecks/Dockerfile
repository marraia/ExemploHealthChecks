FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["ExemploHealthChecks/ExemploHealthChecks.csproj", "ExemploHealthChecks/"]
RUN dotnet restore "ExemploHealthChecks/ExemploHealthChecks.csproj"
COPY . .
WORKDIR "/src/ExemploHealthChecks"
RUN dotnet build "ExemploHealthChecks.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ExemploHealthChecks.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ExemploHealthChecks.dll"]