#Partir d'une image de référence ubuntu en version 24:10
FROM ubuntu:24.10 AS builder
# Installation du SDK dotnet 9
WORKDIR /app
RUN apt-get update && apt-get install -y dotnet-sdk-9.0 ca-certificates net-tools curl
# Ajouter le code source de l'application
WORKDIR /source
COPY . .

WORKDIR /source/my-first-app

# Publication de l'app dotnet
RUN dotnet publish -c Release -o /app

FROM ubuntu:24.10 AS prod
# Récupération des DLL de l'application
WORKDIR /app
COPY --from=builder /app ./
# Installation du SDK dotnet pour un run local
RUN apt-get update && apt-get install -y dotnet-sdk-9.0
# Entrypoint d'exécution de l'application
ENTRYPOINT ["dotnet", "my-first-app.dll"]
