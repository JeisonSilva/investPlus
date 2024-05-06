# Use a imagem oficial do .NET SDK para o build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /source

# Copie o .csproj e restaure as dependências
COPY *.csproj .
RUN dotnet restore

# Copie o resto dos arquivos e faça o build do projeto
COPY . .
RUN dotnet publish -c Release -o /app

# Use a imagem oficial do .NET Runtime para rodar a aplicação
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Copie os arquivos de build do estágio anterior
COPY --from=build /app .

# Exponha a porta que a aplicação utiliza
EXPOSE 8080

# Defina o comando para iniciar a aplicação
ENTRYPOINT ["dotnet", "investPlus.saldoDiario.api.dll"]