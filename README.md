# BrazilAPI Node-RED Integration

[![Node-RED](https://img.shields.io/badge/Node--RED-v4.1.1-red)](https://nodered.org/)
[![BrazilAPI](https://img.shields.io/badge/BrazilAPI-v2-green)](https://brasilapi.com.br/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

🚀 Aplicação Node-RED que integra com a BrazilAPI para fornecer catálogo de corretoras e busca de CEP com mapas interativos.

## 🎥 Demonstração em Vídeo

Assista ao vídeo de demonstração (40 segundos) mostrando todas as funcionalidades:

[![📹 Assistir Demo](https://img.shields.io/badge/▶️-Assistir%20Demonstração-blue?style=for-the-badge)](https://screenapp.io/app/v/7AwZtwR7CV)

**[🎬 Clique aqui para assistir ao vídeo](https://screenapp.io/app/v/7AwZtwR7CV)**

**O vídeo demonstra:**

- ✅ Catálogo de Corretoras com busca em tempo real
- ✅ Busca de CEP por URL (Opção 1)
- ✅ Busca de CEP por formulário (Opção 2)
- ✅ Mapa interativo com geocoding automático
- ✅ Tratamento de erros e validações

## ✨ Funcionalidades Principais

### 📊 1. Catálogo de Corretoras

- 📋 Lista todas as corretoras disponíveis da BrazilAPI
- 🏢 Formato: "Nome - Cidade / CNPJ"
- 🎨 Interface limpa e estilizada
- 🔍 Busca em tempo real por nome, cidade ou CNPJ

### 📍 2. Buscador de CEP

- **🔗 Opção 1**: Via parâmetro de rota (`/cep/:zipcode`)
- **📝 Opção 2**: Formulário com campo de busca
- 🗺️ Exibe endereço completo com mapa interativo
- ⚠️ Tratamento de erros para CEPs inválidos
- 📌 Coordenadas geográficas automáticas

### 🎁 Funcionalidades Bonus

- 🗺️ **Mapas Interativos**: Leaflet.js com markers e popups personalizados
- 🌍 **Geocoding Automático**: Nominatim API para CEPs sem coordenadas
- 🎨 **UI Moderna**: Gradientes, animações e design responsivo
- 📡 **MQTT Integration**: Broker Aedes para mensagens em tempo real
- 💾 **SQLite Database**: Histórico completo de buscas
- ⏳ **Loading States**: Feedback visual durante carregamento
- 🛡️ **Error Handling**: Tratamento robusto de erros e fallbacks

## 🚀 Melhorias Implementadas

### 🗺️ Mapas Interativos com Geocoding Automático

**❌ Problema Identificado:**  
A BrazilAPI nem sempre retorna coordenadas geográficas para todos os CEPs, resultando em páginas sem mapa.

**✅ Solução Implementada:**

1. 🔍 **Detecção Inteligente**: Verifica se a API retornou coordenadas
2. 🌍 **Geocoding Automático**: Se não houver coordenadas, busca via Nominatim (OpenStreetMap)
3. ⏳ **Loading Visual**: Exibe spinner enquanto busca as coordenadas
4. 🛡️ **Fallback Robusto**: Mensagem clara se não for possível obter o mapa

**🔧 Tecnologias Adicionadas:**

- 📚 **Leaflet.js v1.9.4**: Biblioteca open-source de mapas interativos
- 🌐 **Nominatim API**: Serviço de geocoding gratuito do OpenStreetMap
- ⚡ **JavaScript Async/Await**: Para requisições assíncronas

**🎯 Resultado:**

- ✅ **100% dos CEPs válidos** agora exibem mapas interativos
- ✅ Zoom, arrastar e markers clicáveis
- ✅ Experiência consistente para todos os usuários

## 📋 Requisitos

- 🟢 Node.js (v14 ou superior)
- 📦 npm ou yarn

## 🔧 Instalação

**1️⃣ Clone o repositório:**

```bash
git clone https://github.com/mcemy/busca-cep-e-corretores.git
cd busca-cep-e-corretores
```

**2️⃣ Instale o Node-RED globalmente (se ainda não tiver):**

```bash
npm install -g node-red
```

**3️⃣ Instale as dependências Node-RED:**

```bash
npm install node-red-dashboard
npm install node-red-contrib-aedes
npm install node-red-node-sqlite
```

Ou instale via Node-RED Palette Manager:

- 📊 `node-red-dashboard`
- 📡 `node-red-contrib-aedes` (para MQTT)
- 💾 `node-red-node-sqlite` (para database)

**4️⃣ Importe os fluxos:**

- ▶️ Inicie o Node-RED: `node-red`
- 🌐 Abra o navegador: `http://localhost:1880`
- ☰ Vá em Menu → Import
- 📋 Copie o conteúdo de `flows.json` e cole
- ✅ Clique em "Import"

## 🎮 Como Usar

### ▶️ Iniciando a Aplicação

**1️⃣ Inicie o Node-RED:**

```bash
node-red
```

**2️⃣ Aguarde a mensagem:** "Server now running at http://127.0.0.1:1880/"

### 🌐 Acessando as Funcionalidades

#### 📊 Catálogo de Corretoras

- **🔗 URL**: `http://localhost:1880/brokers`
- 📋 Lista todas as corretoras disponíveis da BrazilAPI
- 🔄 Dados carregados automaticamente ao abrir a página
- 🔍 Busca em tempo real por nome, cidade ou CNPJ

#### 📍 Busca de CEP - Opção 1 (Parâmetro de Rota)

- **🔗 URL**: `http://localhost:1880/cep/<zipcode>`
- **📝 Exemplo**: `http://localhost:1880/cep/01310100`
- ✏️ Substitua `<zipcode>` por qualquer CEP brasileiro válido

#### 📍 Busca de CEP - Opção 2 (Formulário)

- **🔗 URL**: `http://localhost:1880/search-cep`
- ✏️ Digite o CEP no campo de busca
- 🔍 Clique no botão "Buscar"
- ✅ Resultados exibidos abaixo com mapa interativo

#### 📊 Dashboard (Bonus)

- **🔗 URL**: `http://localhost:1880/ui`
- 🎨 Dashboard interativo com todas as funcionalidades
- 📡 Atualizações em tempo real via MQTT
- 📜 Visualizador de histórico de buscas

### 📡 Integração MQTT

A aplicação inclui um broker MQTT para atualizações em tempo real:

- **🔌 Broker**: `localhost:1883`
- **📢 Tópicos**:
  - `brazilapi/cep/search` - Publica buscas de CEP
  - `brazilapi/brokers/list` - Publica atualizações da lista de corretoras

**🧪 Para testar o MQTT:**

```bash
# 📥 Subscrever às buscas de CEP
mosquitto_sub -h localhost -t "brazilapi/cep/search"

# 📤 Publicar uma busca de CEP
mosquitto_pub -h localhost -t "brazilapi/cep/search" -m "01310100"
```

### 💾 Database

O histórico de buscas é armazenado em banco SQLite:

- 📂 **Localização**: `~/.node-red/cep_history.db`
- 📊 **Tabela**: `searches` (zipcode, result, timestamp)

## 🧪 Testando a Aplicação

### 📊 Testar Catálogo de Corretoras

1. 🌐 Abra o navegador: `http://localhost:1880/brokers`
2. ✅ Verifique se as corretoras estão listadas no formato: "Nome - Cidade / CNPJ"
3. 🎨 Confirme que o estilo foi aplicado corretamente
4. 🔍 Teste a busca digitando nome, cidade ou CNPJ

### 📍 Testar Busca de CEP - Opção 1

**✅ CEPs válidos para testar:**

```url
http://localhost:1880/cep/01310100  (✅ Av. Paulista, São Paulo)
http://localhost:1880/cep/20040020  (✅ Rio de Janeiro)
http://localhost:1880/cep/30130100  (✅ Belo Horizonte)
```

**❌ CEP inválido (deve mostrar erro):**

```url
http://localhost:1880/cep/00000000
```

### 📍 Testar Busca de CEP - Opção 2

1. 🌐 Abra: `http://localhost:1880/search-cep`
2. ✏️ Digite o CEP: `01310100`
3. 🔍 Clique em "Buscar"
4. ✅ Verifique se os resultados e o mapa aparecem corretamente

### 📊 Testar Dashboard

1. 🌐 Abra: `http://localhost:1880/ui`
2. 🔄 Navegue pelas abas
3. ✅ Teste todas as funcionalidades do dashboard

## 🔌 Endpoints da API

### 📊 GET /brokers

Retorna página HTML com lista de corretoras

### 📍 GET /cep/:zipcode

Retorna página HTML com detalhes do CEP

- **📋 Parâmetro**: zipcode (8 dígitos)

### 📝 GET /search-cep

Retorna página HTML com formulário de busca

### 🔄 POST /api/cep

Retorna JSON com dados do CEP

- **📋 Body**: `{ "cep": "01310100" }`

## 📁 Estrutura do Projeto

```plaintext
busca-cep-e-corretores/
├── 📄 README.md           # Este arquivo
├── 📄 flows.json          # Fluxos do Node-RED
├── 📄 package.json        # Dependências Node.js
├── 📄 package-lock.json   # Versões fixas das dependências
└── 📄 .gitignore          # Arquivos ignorados pelo Git
```

## 🛠️ Stack Técnico

- 🔴 **Node-RED**: Plataforma de programação baseada em fluxos
- 🇧🇷 **BrazilAPI**: API pública de dados brasileiros
- 📡 **MQTT**: Broker Aedes para mensagens em tempo real
- 💾 **SQLite**: Banco de dados local para histórico
- 🗺️ **Leaflet.js**: Mapas interativos
- 🌍 **Nominatim**: Geocoding via OpenStreetMap
- 🎨 **HTML/CSS/JavaScript**: Estilização frontend

## 🔧 Troubleshooting

### ⚠️ Porta já em uso

Se a porta 1880 já estiver em uso, você pode mudá-la:

```bash
node-red -p 1881
```

### ❌ Não consegue conectar ao MQTT

Certifique-se de que o nó broker Aedes está deployed e rodando no fluxo.

### ❌ Erros no Database

O arquivo do banco é criado automaticamente. Se houver problemas:

```bash
rm ~/.node-red/cep_history.db
# Reinicie o Node-RED para recriar
```

### ⚠️ Rate Limiting da API

A BrazilAPI pode limitar requisições. Se encontrar problemas, aguarde alguns momentos entre as requisições.

## 👨‍💻 Desenvolvimento

Para modificar os fluxos:

1. 🌐 Abra o editor Node-RED: `http://localhost:1880`
2. ✏️ Edite os nós e conexões
3. 🚀 Clique em "Deploy" para aplicar as mudanças


## 📝 Notas Importantes

- ✅ Todos os CEPs devem ter 8 dígitos (com ou sem hífen)
- ✅ A aplicação aceita ambos os formatos: 01310-100 ou 01310100
- ✅ Mensagens de erro são exibidas para CEPs inválidos
- ✅ A interface é totalmente responsiva e funciona em dispositivos móveis
- ✅ 100% dos CEPs válidos exibem mapas interativos
- ✅ Geocoding automático para CEPs sem coordenadas na API

```

```
