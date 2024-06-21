## Pré requisitos
- Instalar Atlantis
- Instalar ngrok

## Instruções
1. Criar string aleatória de qualquer tamanho;
2. No seu terminal, crie uma variável ambiente:
```
export SECRET={YOUR_RANDOM_STRING}
```
3. Criar url com Ngrok na porta 4141.
 * O Atlantis precisa ser acessível pelo github, o ngrok expõe sua porta local a um hostname público aleatório. Inicie o ngrok e salve o link gerado:
```
ngrok http 4141
```
4. Crie uma variável ambiente com o link gerado:
```
export URL={YOUR_HOSTNAME}
```
5. No repositório do Github, ir em settings, Webhooks e em Payload URL colocar a URL gerada por `/events` (ex: https://32a5-232-344-123.ngrok-free.app/events)
6. Alterar content type para application/json
7. Adicionar o secret gerado no passo 2
8. Marcar a opção "Let me select individual events" e dar check em:
* Issue Comments
* Pull Request reviews
* Pull Request
* Pushes
9. Criar token de acesso para o Atlantis em Settings > Developer Settings > Personal Access Tokens > Tokens(classic) > Generate new token (classic)
10. Adicione um nome ao token e selecione o escopo 'repo'
11. Salve o token e salve como variável ambiente:
```
export TOKEN={YOUR_TOKEN}
```
12. Exporte seu nome de usuário e o nome do repositório como variáveis ambientes:
```
export USERNAME={YOUR_USERNAME}
export REPO_ALLOWLIST={YOUR_REPO_ALLOWLIST}
```
13. Inicie o Atlantis com o comando:
```
atlantis server \
--atlantis-url="$USERNAME" \
--gh-user="$USERNAME" \
--gh-token="$TOKEN" \
--gh-webhook-secret="$SECRET" \
--repo-allowlist="$REPO_ALLOWLIST"
```

## Aplicando no repositório
1. Abra um PR para iniciar o Atlantis em seu repositório.
2. Para o Apply, comente `Atlantis apply`