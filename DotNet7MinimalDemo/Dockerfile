FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["DotNet7MinimalDemo/DotNet7MinimalDemo.csproj", "DotNet7MinimalDemo/"]
RUN dotnet restore "DotNet7MinimalDemo/DotNet7MinimalDemo.csproj"
COPY . .
WORKDIR "/src/DotNet7MinimalDemo"
RUN dotnet build "DotNet7MinimalDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DotNet7MinimalDemo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotNet7MinimalDemo.dll"]
