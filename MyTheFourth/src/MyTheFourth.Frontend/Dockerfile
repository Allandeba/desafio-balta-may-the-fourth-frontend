# Estágio de publicação
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
EXPOSE 80
WORKDIR /src
COPY MyTheFourth.Frontend.csproj .
RUN dotnet restore MyTheFourth.Frontend.csproj
COPY . .
RUN dotnet build MyTheFourth.Frontend.csproj -c Release -o /app/build

# Estágio de publicação
FROM build AS publish
RUN dotnet publish "MyTheFourth.Frontend.csproj" -c Release -o /app/publish

# Etapa final
FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
COPY --from=publish /app/publish/wwwroot .
COPY nginx.conf /etc/nginx/nginx.conf
