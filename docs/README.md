# solvaholic/huginn
Here's where @solvaholic scratches the "want to use Huginn" itch by learning Ruby on Rails

## Helpful resources

- [_huginn/README.md_](https://github.com/huginn/huginn/blob/master/README.md)
- [_huginn/doc/docker/install.md_](https://github.com/huginn/huginn/blob/master/doc/docker/install.md)
- [_Rails Crash Course_](https://nostarch.com/railscrashcourse) from no starch press

## Up and running with Huginn

### 1. Create your `.env` file

Copy `.env.example` to `.env`, read through it, and set your settings. In particular, be sure to set these:

- `APP_SECRET_TOKEN`

    @radavis' [_Generate Secret Keys_](https://radavis.github.io/ruby/generate-secret-keys/) explains how to generate one

- `DATABASE_PASSWORD`

    Set this to a random string, for example the output of:
    ```
    openssl rand -base64 12
    ```

- `RAILS_ENV`
- `INVITATION_CODE`
- `SMTP_*`
- `EMAIL_FROM_ADDRESS`

    This will be used if `RAILS_ENV` is `production` or `SEND_EMAIL_IN_DEVELOPMENT` is `true`.

### 2. Run Huginn
If you're already using Docker locally, Huginn is super simple to run:

```bash
docker run --detach --rm --name huginn --env-file .env \
-p 3000:3000 -v huginn_data:/var/lib/mysql huginn/huginn
```

If you're not already using Docker locally, start using it.

| OS | Install Docker |
|:- |:- |
| macOS | `brew install --cask docker` |
| LInux | [_Install Docker Engine_](https://docs.docker.com/engine/install/#server) |
| Windows | Install [Docker Desktop](https://www.docker.com/products/docker-desktop) |

## GitHub Actions workflows in this repository

### Lint Code Base

Runs **[github/super-linter](https://github.com/github/super-linter)** on each push to this repository, and adds the resulting status to the commit.

View or modify this workflow's configuration in `.github/workflows/linter.yml`.

### Sync changes from template

Periodically checks for changes in **[solvaholic/template](https://github.com/solvaholic/template)** and, if there are any, creates or updates a pull request in this repository to review the changes.

View or modify this workflow's configuration in `.github/workflows/sync-from-template.yml`.
