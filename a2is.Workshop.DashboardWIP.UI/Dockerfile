#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["a2is.Workshop.DashboardWIP.UI/a2is.Workshop.DashboardWIP.UI.csproj", "a2is.Workshop.DashboardWIP.UI/"]
RUN dotnet restore "a2is.Workshop.DashboardWIP.UI/a2is.Workshop.DashboardWIP.UI.csproj"
COPY . .
WORKDIR "/src/a2is.Workshop.DashboardWIP.UI"
RUN dotnet build "a2is.Workshop.DashboardWIP.UI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "a2is.Workshop.DashboardWIP.UI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish/ .
ENTRYPOINT ["dotnet", "a2is.Workshop.DashboardWIP.UI.dll"]