# Utilizar la imagen de SDK de .NET Core para construir
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /app

# Copiar solo el archivo de solución y restaurar las dependencias
COPY myLPApp.sln .
RUN dotnet restore

# Copiar todo el código fuente y construir la aplicación
COPY . .
RUN dotnet build -c Release

# Publicar la aplicación
RUN dotnet publish -c Release -o out

# Utilizar una imagen más ligera para la ejecución
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS runtime
WORKDIR /app
COPY --from=build /app/out .

# Establecer el comando de inicio
ENTRYPOINT ["dotnet", "myLPApp.sln"]
