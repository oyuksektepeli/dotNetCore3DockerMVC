#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["./dotNetCore3DockerMVC/dotNetCore3DockerMVC.csproj", "./dotNetCore3DockerMVC/"]
RUN dotnet restore "dotNetCore3DockerMVC/dotNetCore3DockerMVC.csproj"
COPY . ./dotNetCore3DockerMVC
WORKDIR "/src/dotNetCore3DockerMVC"
RUN dotnet build "dotNetCore3DockerMVC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotNetCore3DockerMVC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotNetCore3DockerMVC.dll"]
