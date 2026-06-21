DEPLOY — Ручной деплой сайта

Кратко
- Автоматические деплои отключены/отключайте в Cloudflare Pages (Disconnect repository) — тогда пуши из Git не будут деплоить сайт автоматически.
- Для ручного деплоя используйте Cloudflare Dashboard или `wrangler` (CLI).

1) Отключить автодеплой (Cloudflare Pages)
- Cloudflare → Pages → выберите проект → Settings → Git → Disconnect repository

2) Ручной деплой через Dashboard
- Pages → Deployments → нажать "Upload" / "Publish" (интерфейс позволяет загрузить готовую сборку).

3) Ручной деплой через Wrangler (CLI)
Установка (нужно Node.js и npm):
```bash
npm install -g wrangler
```
Авторизация (в браузере):
```bash
wrangler login
```
Или с API-токеном (создайте Token в Cloudflare с нужными правами):
```bash
wrangler config <API_TOKEN>
```

Publish для Workers (если сайт = Worker):
```bash
wrangler publish
```

Publish для Pages (публикация каталога сборки):
```bash
# пример: у вас есть готовая сборка в ./out
wrangler pages publish ./out --project-name=oleg-k
```

4) Токены и права
- Для `wrangler publish` и `pages publish` нужен API token с правами Pages:Edit или Workers Scripts:Edit и Accounts:Read. Создавайте токен через Cloudflare Dashboard → My Profile → API Tokens → Create Token.
- Никогда не публикуйте токен в открытый доступ.

5) Отключение автоматик на стороне GitHub (по желанию)
- GitHub → репо → Settings → Webhooks → удалить webhook на Cloudflare
- GitHub → репо → Settings → Actions → Disable Actions for this repository (если хотите полностью запретить workflows)
- Или удалить `.github/workflows/*` из репозитория

6) Рекомендации безопасности
- Сделайте репозиторий приватным, если не хотите, чтобы другие клонировали и деплоили ваш сайт.
- Убедитесь, что deploy-keys и секреты удалены/ограничены, если больше не нужны.

7) Быстрые заметки
- Если нужно удалить уже опубликованный Worker/Pages-проект через API — скажите, и я подготовлю пример curl-команды с шаблонами для `{ACCOUNT_ID}`, `{SCRIPT_NAME}` и т.п. (не отправляйте токены в чат).

---
Файл создан автоматически. Если хотите, я добавлю примеры для вашей конкретной структуры сборки (какая папка содержит собранный сайт: `./out`, `./dist` и т.п.).