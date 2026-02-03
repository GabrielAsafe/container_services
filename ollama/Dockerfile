FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Instalar dependências de sistema
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    git \
    curl \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Clonar o WebUI
RUN git clone https://github.com/oobabooga/text-generation-webui /opt/webui

# Instalar dependências CPU‑only
RUN cd /opt/webui \
    && pip3 install --upgrade pip \
    && pip3 install -r requirements/portable/requirements_cpu_only.txt

# Criar diretório de trabalho
WORKDIR /root/webui_data

# Expor porta da WebUI
EXPOSE 7860

# Comando para iniciar a WebUI
CMD ["bash", "-c", "cd /opt/webui && python3 server.py --portable --listen --listen-port 7860 --listen-host 0.0.0.0"]
