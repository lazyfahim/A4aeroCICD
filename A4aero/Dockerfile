#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["A4aero/A4aero.csproj", "A4aero/"]
RUN dotnet restore "A4aero/A4aero.csproj"
COPY . .
WORKDIR "/src/A4aero"
RUN dotnet build "A4aero.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "A4aero.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "A4aero.dll"]