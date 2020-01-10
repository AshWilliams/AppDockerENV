FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-alpine AS build
WORKDIR /src
COPY ["tailwind-frontend.csproj", ""]
RUN dotnet restore "tailwind-frontend.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "tailwind-frontend.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "tailwind-frontend.csproj" -c Release -o /app

FROM base AS final
ENV ConnectionString=BDConnStringFromENV
ENV endPoint=http://fromenv:52237/coolapi/tailwind
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "tailwind-frontend.dll"]