---
name: make-changelog
description: Gerencia entradas no CHANGELOG.md seguindo Keep a Changelog. Use em Codex quando versões, scripts, documentação ou skills mudarem e for necessário registrar Added, Changed, Fixed ou Removed.
---

# Make Changelog

Use esta skill para manter `CHANGELOG.md` preciso, legível e consistente com as versões de `desktop.sh` e `server.sh`.

## Plataforma

Esta é a versão Codex da skill.

- Use `exec_command` para `git log`, `git diff`, `git status` e validações.
- Use `rg` para localizar versões, steps e referências relacionadas.
- Use `apply_patch` para atualizar arquivos.
- Use a skill `markdown-format` após alterar Markdown.

## Coleta de Mudanças

Antes de escrever, identifique exatamente o que mudou desde a última versão:

- Use `git log vANTERIOR..HEAD --oneline` quando houver uma tag anterior clara.
- Use `git diff vANTERIOR..HEAD --stat` quando o histórico não explicar o impacto.
- Verifique mudanças nas funções `step_NN_` em `desktop.sh` e `server.sh`.
- Verifique alterações em `AGENTS.md`, `CLAUDE.md`, `.codex/skills` e `.claude/skills`.

## Categorias

Distribua as mudanças nas seções padronizadas:

- **Added:** novos recursos, ferramentas, aliases, docs ou skills.
- **Changed:** mudanças em comportamento, fluxo, documentação ou dependências.
- **Fixed:** correções de bugs, permissões, paths, links ou edge cases.
- **Removed:** recursos, ferramentas, arquivos, contextos ou skills removidos.

## Formato

- Use H2 com versão e data: `## [v0.42.0] - 2026-04-10`.
- Coloque o novo bloco no topo, abaixo do cabeçalho principal.
- Use bullets com `-`.
- Mantenha uma linha em branco entre categorias.
- Preserve histórico existente.

## Checklist

- [ ] A versão coincide com `VERSION` em `desktop.sh` e `server.sh`.
- [ ] A data do bloco está correta.
- [ ] O bloco novo está no topo.
- [ ] Contextos ativos e skills estão citados quando afetados.
- [ ] `markdown-format` foi aplicado.
