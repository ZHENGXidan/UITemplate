#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["UITemplate.Core/UITemplate.Core.csproj", "UITemplate.Core/"]
RUN dotnet restore "UITemplate.Core/UITemplate.Core.csproj"
COPY . .
WORKDIR "/src/UITemplate.Core"
RUN dotnet build "UITemplate.Core.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "UITemplate.Core.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "UITemplate.Core.dll"]