#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Test5/Test5.csproj", "Test5/"]
RUN dotnet restore "Test5/Test5.csproj"
COPY . .
WORKDIR "/src/Test5"
RUN dotnet build "Test5.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Test5.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Test5.dll"]