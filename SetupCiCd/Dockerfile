FROM mcr.microsoft.com/dotnet/sdk:10.0-preview AS build
WORKDIR /src

COPY ["SetupCiCd.csproj", "./"]
RUN dotnet restore "SetupCiCd.csproj"

COPY . .
RUN dotnet build "SetupCiCd.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SetupCiCd.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:10.0-preview AS final
WORKDIR /app
EXPOSE 8080
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SetupCiCd.dll"]
