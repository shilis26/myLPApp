# Utilizar la imagen de SDK de .NET Core para construir
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /app

# Copiar solo el archivo de soluci�n y restaurar las dependencias
COPY myLPApp.sln .
RUN dotnet restore

# Copiar todo el c�digo fuente y construir la aplicaci�n
COPY . .
RUN dotnet build -c Release

# Publicar la aplicaci�n
RUN dotnet publish -c Release -o out

# Utilizar una imagen m�s ligera para la ejecuci�n
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS runtime
WORKDIR /app
COPY --from=build /app/out .

# Establecer el comando de inicio
ENTRYPOINT ["dotnet", "myLPApp.sln"]
