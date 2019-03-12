FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["MyK8sApp/MyK8sApp.csproj", "MyK8sApp/"]

RUN dotnet restore "MyK8sApp/MyK8sApp.csproj"
COPY . .
WORKDIR "/src/MyK8sApp"
RUN dotnet build "MyK8sApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MyK8sApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MyK8sApp.dll"]