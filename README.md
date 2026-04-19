# GitHub Actions Runners - Docker Setup

Este projeto permite rodar múltiplos runners do GitHub Actions localmente usando Docker, com suporte para escalabilidade e isolamento.

## Configuração Inicial

1.  **Crie o arquivo `.env`**:
    ```bash
    cp .env.example .env
    ```

2.  **Configure suas credenciais**:
    Edite o arquivo `.env` e preencha com:
    - `GITHUB_PAT`: Seu Personal Access Token (necessita escopos `repo`, `admin:org`, `workflow`).
    - `ORG_NAME`: Nome da sua organização no GitHub.
    - `PERSONAL_REPO_URL`: URL do repositório pessoal que deseja atender.

## Como Executar

### Subir um runner de cada tipo
```bash
docker-compose up -d
```

### Escalar (Rodar múltiplos runners)
Para rodar, por exemplo, 3 instâncias do runner de organização:
```bash
docker-compose up -d --scale org-runner=3
```

### Parar tudo
```bash
docker-compose down
```

## Monitoramento
Você pode ver os logs dos runners em tempo real com:
```bash
docker-compose logs -f
```

E conferir no painel do GitHub:
- **Org**: Settings > Actions > Runners
- **Repo**: Settings > Actions > Runners

## Observações de Segurança
- Runners "Self-hosted" em repositórios **públicos** são um risco de segurança. Use apenas em repositórios **privados**.
- O uso do `docker.sock` permite que os runners executem comandos Docker, mas dá ao container privilégios de root no host Docker.
