---
name: documentation
description: Workflow mestre para gestão de documentação do SetupVibe. Use ao criar, revisar, traduzir ou sincronizar Markdown, READMEs, CHANGELOG e documentação de steps em Codex.
---

# Documentation Workflow

Use esta skill para manter a documentação do SetupVibe sincronizada, traduzida e compatível com os padrões do projeto.

## Plataforma

Esta é a versão Codex da skill.

- Use `rg` ou `rg --files` para localizar arquivos e referências.
- Use `apply_patch` para edições manuais em Markdown.
- Use `exec_command` para verificações como `git diff`, `markdownlint`, `ls` e `rg`.
- Mantenha `.codex/skills` alinhada com `.claude/skills`, preservando instruções específicas de Codex.

## Fonte de Verdade

- Regras de Markdown: [`MARKDOWN.md`](../../../MARKDOWN.md).
- Configuração markdownlint: [`.markdownlint.json`](../../../.markdownlint.json).
- Contextos ativos: [`AGENTS.md`](../../../AGENTS.md) e [`CLAUDE.md`](../../../CLAUDE.md).

## Fluxo

1. Leia os arquivos relacionados antes de editar.
2. Quando `desktop.sh` ou `server.sh` mudarem, atualize as seções correspondentes no `README.md` da raiz e nos READMEs relevantes em todos os idiomas.
3. Quando a versão mudar, atualize `desktop.sh`, `server.sh`, `CHANGELOG.md`, `README.md`, `AGENTS.md`, `CLAUDE.md` e os READMEs em `docs/`.
4. Use inglês (`docs/en`) como fonte de verdade para traduções.
5. Não traduza comandos, aliases, nomes de pacote, paths ou variáveis de ambiente.
6. Verifique links relativos com `ls` ou leitura direta do arquivo de destino.
7. Rode a verificação da skill `markdown-format` antes de concluir.

## Checklist Final

- [ ] Os arquivos alterados seguem `MARKDOWN.md`.
- [ ] `AGENTS.md` e `CLAUDE.md` continuam sincronizados nas regras compartilhadas.
- [ ] `.codex/skills` e `.claude/skills` continuam funcionalmente equivalentes.
- [ ] Não há novas referências a agentes fora de Codex e Claude como contexto ou pasta de skills ativa.
