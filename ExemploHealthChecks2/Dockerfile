FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["ExemploHealthChecks2/ExemploHealthChecks2.csproj", "ExemploHealthChecks2/"]
RUN dotnet restore "ExemploHealthChecks2/ExemploHealthChecks2.csproj"
COPY . .
WORKDIR "/src/ExemploHealthChecks2"
RUN dotnet build "ExemploHealthChecks2.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ExemploHealthChecks2.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ExemploHealthChecks2.dll"]