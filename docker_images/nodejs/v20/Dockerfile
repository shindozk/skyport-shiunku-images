# Use a imagem slim do Node.js 20, ajustada para a arquitetura de destino
FROM --platform=$TARGETOS/$TARGETARCH node:20-bullseye-slim

# Atualiza e instala dependências necessárias
RUN apt update \
    && apt -y install ffmpeg iproute2 git sqlite3 libsqlite3-dev python3 python3-dev ca-certificates dnsutils tzdata zip tar curl build-essential libtool

# Atualiza o npm para a versão mais recente
RUN npm install npm@latest -g

# Define o diretório de trabalho como /app/data/
WORKDIR /app/data

# Adiciona o script de inicialização diretamente no Dockerfile
RUN echo '#!/bin/bash \n\
# Exibe a versão do Node.js \n\
node -v \n\
# Mostra o comando START configurado pelo usuário \n\
echo ":/app/data$ ${START}" \n\
# Substitui e executa o comando START \n\
eval ${START}' > /entrypoint.sh && chmod +x /entrypoint.sh

# Define o comando padrão para o container
CMD ["sh", "/entrypoint.sh"]
