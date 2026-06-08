# Chatbot de Temperatura via Telegram com N8N

## Descrição

Este projeto implementa um chatbot no Telegram utilizando o N8N que consulta a temperatura atual de uma cidade informada pelo usuário e retorna uma resposta formatada em português.

### Exemplo de uso

**Entrada do usuário:**

```text
Salvador,BA,BR
```

**Resposta do bot:**

```text
🌤️ A temperatura em Salvador é de 27°C.
```

## Arquivos do Projeto

Obrigatórios:

- workflow-chatbot-telegram.json
- README.md

Opcional:

- docker-compose.yml

## Observação Importante sobre a API OpenWeather

O enunciado solicita o endpoint:

https://api.openweathermap.org/data/2.5/weather

Entretanto, nesta implementação foi utilizada a versão mais recente da API One Call Current:

https://api.openweathermap.org/data/4.0/onecall/current

Como esse endpoint exige latitude e longitude ao invés do nome da cidade, foi necessário adicionar uma etapa prévia utilizando o serviço de geocodificação da OpenWeather:

http://api.openweathermap.org/geo/1.0/direct

Fluxo utilizado:

Cidade -> Geocoding -> Latitude/Longitude -> One Call Current -> Temperatura

## Variáveis de Ambiente

```env
OPENWEATHER_API_KEY=sua_chave_aqui
TELEGRAM_BOT_TOKEN=seu_token_aqui
```

## Importação

1. Abra o N8N.
2. Clique em Import from File.
3. Selecione `workflow-chatbot-telegram.json`.
4. Configure as credenciais do Telegram e OpenWeather.
5. Ative o workflow.

## Testes

- Salvador,BA,BR
- São Paulo,SP,BR
- Belo Horizonte,MG,BR

Cidade inválida:

```text
cidade_inexistente
```

Resposta esperada:

```text
❌ Cidade não encontrada. Use o formato Cidade,UF,BR (ex.: São Paulo,SP,BR).
```
