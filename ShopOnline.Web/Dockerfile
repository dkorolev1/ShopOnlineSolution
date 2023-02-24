FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ShopOnline.Web/ShopOnline.Web.csproj", "ShopOnline.Web/"]
COPY ["ShopOnline.Models/ShopOnline.Models.csproj", "ShopOnline.Models/"]
RUN dotnet restore "ShopOnline.Web/ShopOnline.Web.csproj"
COPY . .
WORKDIR "/src/ShopOnline.Web"
RUN dotnet build "ShopOnline.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ShopOnline.Web.csproj" -c Release -o /app/publish

FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
COPY --from=publish /app/publish/wwwroot .
COPY ShopOnline.Web/nginx.conf /etc/nginx/nginx.conf  