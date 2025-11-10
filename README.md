# 🇧🇷 BrazilAPI Node-RED Integration

[![Node-RED](https://img.shields.io/badge/Node--RED-v4.1.1-red)](https://nodered.org/)
[![BrazilAPI](https://img.shields.io/badge/BrazilAPI-v2-green)](https://brasilapi.com.br/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

Aplicação Node-RED que integra com a BrazilAPI para fornecer catálogo de corretoras e busca de CEP com mapas interativos.

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

## ✨ Features

### 1. Broker Catalog

- Lists all available brokers from BrazilAPI
- Format: "Name - City / CNPJ"
- Clean, styled interface

### 2. Zip Code Searcher

- **Option 1**: Route parameter (`/cep/:zipcode`)
- **Option 2**: Input field with search button
- Displays complete address details
- Error handling for invalid zip codes

### 🎁 Bonus Features

- **Mapas Interativos**: Leaflet.js com markers e popups personalizados
- **Geocoding Automático**: Nominatim API para CEPs sem coordenadas
- **UI Moderna**: Gradientes, animações e design responsivo
- **MQTT Integration**: Broker Aedes para mensagens em tempo real
- **SQLite Database**: Histórico completo de buscas
- **Loading States**: Feedback visual durante carregamento
- **Error Handling**: Tratamento robusto de erros e fallbacks

## 🚀 Melhorias Implementadas

### Mapas Interativos com Geocoding Automático

**Problema Identificado:**
A BrazilAPI nem sempre retorna coordenadas geográficas para todos os CEPs, resultando em páginas sem mapa.

**Solução Implementada:**

1. **Detecção Inteligente**: Verifica se a API retornou coordenadas
2. **Geocoding Automático**: Se não houver coordenadas, busca via Nominatim (OpenStreetMap)
3. **Loading Visual**: Exibe spinner enquanto busca as coordenadas
4. **Fallback Robusto**: Mensagem clara se não for possível obter o mapa

**Tecnologias Adicionadas:**

- **Leaflet.js v1.9.4**: Biblioteca open-source de mapas interativos
- **Nominatim API**: Serviço de geocoding gratuito do OpenStreetMap
- **JavaScript Async/Await**: Para requisições assíncronas

**Resultado:**
✅ **100% dos CEPs válidos** agora exibem mapas interativos  
✅ Zoom, arrastar e markers clicáveis  
✅ Experiência consistente para todos os usuários

## Requirements

- Node.js (v14 or higher)
- npm or yarn

## Installation

1. Clone the repository:

```bash
git clone <your-repo-url>
cd nodered-brazilapi
```

2. Install Node-RED globally (if not already installed):

```bash
npm install -g node-red
```

3. Install required Node-RED nodes:

```bash
npm install node-red-dashboard
npm install node-red-contrib-aedes
npm install node-red-node-sqlite
```

Or install via Node-RED Palette Manager:

- node-red-dashboard
- node-red-contrib-aedes (for MQTT)
- node-red-node-sqlite (for database)

4. Import the flows:

- Start Node-RED: `node-red`
- Open browser: `http://localhost:1880`
- Go to Menu (☰) → Import
- Copy the content from `flows.json` and paste it
- Click "Import"

## Usage

### Starting the Application

1. Start Node-RED:

```bash
node-red
```

2. Wait for the message: "Server now running at http://127.0.0.1:1880/"

### Accessing the Features

#### Broker Catalog

- **URL**: `http://localhost:1880/brokers`
- Lists all available brokers from BrazilAPI
- Automatically fetches data on page load

#### Zip Code Searcher - Option 1 (Route Parameter)

- **URL**: `http://localhost:1880/cep/<zipcode>`
- Example: `http://localhost:1880/cep/01310100`
- Replace `<zipcode>` with any valid Brazilian zip code

#### Zip Code Searcher - Option 2 (Input Field)

- **URL**: `http://localhost:1880/search-cep`
- Enter zip code in the input field
- Click "Search" button
- Results display below

#### Dashboard (Bonus)

- **URL**: `http://localhost:1880/ui`
- Interactive dashboard with both features
- Real-time MQTT updates
- Search history viewer

### MQTT Integration

The application includes an MQTT broker for real-time updates:

- **Broker**: `localhost:1883`
- **Topics**:
  - `brazilapi/cep/search` - Publishes CEP searches
  - `brazilapi/brokers/list` - Publishes broker list updates

To test MQTT:

```bash
# Subscribe to CEP searches
mosquitto_sub -h localhost -t "brazilapi/cep/search"

# Publish a CEP search
mosquitto_pub -h localhost -t "brazilapi/cep/search" -m "01310100"
```

### Database

Search history is stored in SQLite database:

- Location: `~/.node-red/cep_history.db`
- Table: `searches` (zipcode, result, timestamp)

## Testing

### Test Broker Catalog

1. Open browser: `http://localhost:1880/brokers`
2. Verify that brokers are listed in format: "Name - City / CNPJ"
3. Check that styling is applied

### Test CEP Search - Option 1

Valid zip codes to test:

```
http://localhost:1880/cep/01310100  (Av. Paulista, São Paulo)
http://localhost:1880/cep/20040020  (Rio de Janeiro)
http://localhost:1880/cep/30130100  (Belo Horizonte)
```

Invalid zip code (should show error):

```
http://localhost:1880/cep/00000000
```

### Test CEP Search - Option 2

1. Open: `http://localhost:1880/search-cep`
2. Enter zip code: `01310100`
3. Click "Search"
4. Verify results display correctly

### Test Dashboard

1. Open: `http://localhost:1880/ui`
2. Navigate through tabs
3. Test all features in the dashboard interface

## API Endpoints

### GET /brokers

Returns HTML page with broker list

### GET /cep/:zipcode

Returns HTML page with CEP details

- **Parameter**: zipcode (8 digits)

### GET /search-cep

Returns HTML page with search form

### POST /api/cep

Returns JSON with CEP data

- **Body**: `{ "cep": "01310100" }`

## Project Structure

```
nodered-brazilapi/
├── README.md           # This file
├── flows.json          # Node-RED flows
├── package.json        # Node.js dependencies
└── screenshots/        # Application screenshots (optional)
```

## Technical Stack

- **Node-RED**: Flow-based programming platform
- **BrazilAPI**: Brazilian public data API
- **MQTT**: Aedes broker for real-time messaging
- **SQLite**: Local database for history
- **HTML/CSS/JavaScript**: Frontend styling
- **Node-RED Dashboard**: UI framework

## Troubleshooting

### Port already in use

If port 1880 is already in use, you can change it:

```bash
node-red -p 1881
```

### Cannot connect to MQTT

Ensure the Aedes broker node is deployed and running in the flow.

### Database errors

The database file is created automatically. If issues occur:

```bash
rm ~/.node-red/cep_history.db
# Restart Node-RED to recreate
```

### API Rate Limiting

BrazilAPI may rate limit requests. If you encounter issues, wait a few moments between requests.

## Development

To modify the flows:

1. Open Node-RED editor: `http://localhost:1880`
2. Edit nodes and connections
3. Click "Deploy" to apply changes

## License

MIT

## Author

Created as a technical assessment project.

## Notes

- All zip codes should be 8 digits (with or without hyphen)
- The application handles both formats: 01310-100 or 01310100
- Error messages are displayed for invalid zip codes
- The UI is fully responsive and works on mobile devices

```

```
