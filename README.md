# README: Instalando Docker no Fedora

Este guia explica **como instalar o Docker CE (Community Edition) no Fedora moderno**, configurar para uso sem `sudo` e testar a instalação.

---

## 1️⃣ Remover versões antigas do Docker

```bash
sudo dnf remove -y docker \
  docker-client \
  docker-client-latest \
  docker-common \
  docker-latest \
  docker-latest-logrotate \
  docker-logrotate \
  docker-selinux \
  docker-engine-selinux \
  docker-engine
```
**Explicação:**
- `sudo` → executa como administrador  
- `dnf remove -y` → remove pacotes e responde “sim” automaticamente  
- Lista de pacotes → possíveis versões antigas do Docker que podem causar conflito  
- `\` → permite quebrar o comando em várias linhas para melhor leitura

💡 Objetivo: Garantir que **não haja conflitos** com versões antigas.

---

## 2️⃣ Instalar plugin do DNF

```bash
sudo dnf install -y dnf-plugins-core
```
**Explicação:**
- Instala plugins adicionais do DNF, incluindo ferramentas para gerenciar repositórios.  
- `-y` → responde “sim” automaticamente

💡 Objetivo: Necessário para adicionar repositórios externos.

---

## 3️⃣ Criar repositório oficial do Docker

```bash
sudo tee /etc/yum.repos.d/docker-ce.repo > /dev/null <<EOF
[docker-ce-stable]
name=Docker CE Stable - \$basearch
baseurl=https://download.docker.com/linux/fedora/\$releasever/\$basearch/stable
enabled=1
gpgcheck=1
gpgkey=https://download.docker.com/linux/fedora/gpg
EOF
```
**Explicação linha a linha:**
- `sudo tee /etc/yum.repos.d/docker-ce.repo > /dev/null` → cria um arquivo de repositório no local correto  
- `[docker-ce-stable]` → identificador interno do repositório  
- `name=` → nome amigável  
- `baseurl=` → URL de onde baixar os pacotes  
- `enabled=1` → ativa o repositório  
- `gpgcheck=1` → verifica assinatura dos pacotes  
- `gpgkey=` → chave para validar pacotes

💡 Objetivo: Permitir que o Fedora conheça o repositório oficial do Docker.

---

## 4️⃣ Instalar Docker e ferramentas relacionadas

```bash
sudo dnf install -y \
  docker-ce \
  docker-ce-cli \
  containerd.io \
  docker-buildx-plugin \
  docker-compose-plugin
```
**Explicação dos pacotes:**
- `docker-ce` → motor principal do Docker  
- `docker-ce-cli` → interface de linha de comando (`docker`)  
- `containerd.io` → runtime de containers usado pelo Docker  
- `docker-buildx-plugin` → plugin para builds avançados (multi-plataforma)  
- `docker-compose-plugin` → plugin oficial para `docker compose up`  

💡 Objetivo: Instalar tudo que o Docker moderno precisa para rodar containers e gerenciar stacks.

---

## 5️⃣ Iniciar e ativar o serviço Docker

```bash
sudo systemctl enable --now docker
```
**Explicação:**
- `systemctl` → gerenciador de serviços do Linux (systemd)  
- `enable` → inicia automaticamente no boot  
- `--now` → inicia imediatamente  
- `docker` → nome do serviço  

💡 Objetivo: Docker já iniciado e ativo no boot.

---

## 6️⃣ Usar Docker sem `sudo`

```bash
sudo usermod -aG docker $USER
```
**Explicação:**
- `usermod` → modifica usuários  
- `-aG docker` → adiciona o usuário ao grupo `docker`  
- `$USER` → seu usuário atual  

💡 Objetivo: permitir rodar `docker` sem precisar de `sudo`.

**Importante:** Após executar, faça logout/login ou rode:
```bash
newgrp docker
```
para aplicar o grupo na sessão atual.

---

## 7️⃣ Testar instalação

```bash
docker run hello-world
```
**Explicação:**
- `docker run` → roda um container temporário  
- `hello-world` → imagem de teste do Docker  
- Se aparecer a mensagem de teste → ✅ Docker funcionando

---

## 8️⃣ Notas adicionais para Fedora / SELinux

- O Fedora ativa SELinux por padrão  
- Se for usar **volumes em containers**, às vezes é necessário adicionar `:Z` no volume, ex:  

```yaml
volumes:
  - ollama:/root/.ollama:Z
```
- `:Z` ajusta automaticamente o contexto SELinux para permitir acesso do container

💡 Objetivo: evitar problemas de permissão em containers.

---

## ✅ Conclusão

Agora você tem:
- Docker CE instalado no Fedora  
- Serviço rodando e ativo no boot  
- Usuário configurado para rodar Docker sem `sudo`  
- Teste `hello-world` confirmando que funciona  

Pronto para **subir containers LLM como Ollama + Open WebUI**.

