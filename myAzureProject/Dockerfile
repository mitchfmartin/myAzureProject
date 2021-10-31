FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["myAzureProject/myAzureProject.csproj", "myAzureProject/"]

RUN dotnet restore "myAzureProject/myAzureProject.csproj"
COPY . .
WORKDIR "/src/myAzureProject"
RUN dotnet build "myAzureProject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "myAzureProject.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "myAzureProject.dll"]