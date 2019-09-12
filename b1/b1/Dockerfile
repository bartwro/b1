FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["b1/b1.csproj", "b1/"]
RUN dotnet restore "b1/b1.csproj"
COPY . .
WORKDIR "/src/b1"
RUN dotnet build "b1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "b1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "b1.dll"]