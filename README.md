# claude-skills

Ce repo est une **marketplace de plugins Claude Code** privée. Il sert à versionner mes skills Claude et à les synchroniser entre mes machines via GitHub.

Il contient un plugin, `mes-skills`, qui regroupe les skills.

```
claude-skills/
├── .claude-plugin/
│   └── marketplace.json        # catalogue de la marketplace
└── plugins/
    └── mes-skills/
        ├── .claude-plugin/
        │   └── plugin.json     # manifeste du plugin
        └── skills/
            └── <nom-skill>/
                └── SKILL.md
```

## Installation sur une autre machine

Le repo est privé : Git doit pouvoir s'authentifier auprès de GitHub sur la machine. Avec GitHub CLI :

```
gh auth login
gh auth setup-git
```

Puis, dans Claude Code :

```
/plugin marketplace add U3Lab/claude-skills
/plugin install mes-skills@claude-skills
```

## Ajouter une skill

1. Créer `plugins/mes-skills/skills/<nom>/SKILL.md`, avec `<nom>` en kebab-case et ce frontmatter :

   ```markdown
   ---
   name: <nom>
   description: "Ce que fait la skill, et les demandes qui doivent la déclencher."
   ---

   Instructions de la skill.
   ```

2. Augmenter le numéro de version (par exemple `0.1.0` → `0.2.0`) dans **les deux** fichiers, avec la même valeur :
   - `plugins/mes-skills/.claude-plugin/plugin.json`
   - `.claude-plugin/marketplace.json`
3. Ajouter la skill au tableau ci-dessous, et une ligne datée dans `CHANGELOG.md`.
4. Commit et push (avec Claude, suivre le parcours de `CLAUDE.md`, qui demande un accord avant cette étape) :

   ```
   git add .
   git commit -m "feat: add <nom> skill"
   git push
   ```

5. Sur chaque machine, dans Claude Code :

   ```
   /plugin marketplace update claude-skills
   ```

   Si la nouvelle version du plugin n'est pas prise en compte, le mettre à jour depuis le menu `/plugin`, puis redémarrer Claude Code.

La même montée de version s'applique quand on modifie une skill existante.

## Skills du plugin `mes-skills`

| Nom | Description |
| --- | --- |
| `exemple-skill` | Skill d'exemple, pour vérifier que le plugin est bien chargé. À remplacer. |
