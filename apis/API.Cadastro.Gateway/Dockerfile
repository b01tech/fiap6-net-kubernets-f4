# Etapa 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copia os arquivos do projeto e restaura depend�ncias
COPY src/Cadastro.Gateway.API/Cadastro.Gateway.API.csproj ./Cadastro.Gateway.API/
RUN dotnet restore Cadastro.Gateway.API/Cadastro.Gateway.API.csproj

# Copia o c�digo restante e compila a aplica��o
COPY src/Cadastro.Gateway.API/. ./Cadastro.Gateway.API/
WORKDIR /app/Cadastro.Gateway.API
RUN dotnet publish -c Release -o /out

# Etapa 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /out ./

# Exp�e a porta que o servi�o utiliza
EXPOSE 8080
ENTRYPOINT ["dotnet", "Cadastro.Gateway.API.dll"]
