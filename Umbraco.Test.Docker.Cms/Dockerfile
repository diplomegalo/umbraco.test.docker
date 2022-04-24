FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Umbraco.Test.Docker.Cms/Umbraco.Test.Docker.Cms.csproj", "Umbraco.Test.Docker.Cms/"]
RUN dotnet restore "Umbraco.Test.Docker.Cms/Umbraco.Test.Docker.Cms.csproj"
COPY . .
WORKDIR "/src/Umbraco.Test.Docker.Cms"
RUN dotnet build "Umbraco.Test.Docker.Cms.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Umbraco.Test.Docker.Cms.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Umbraco.Test.Docker.Cms.dll"]
