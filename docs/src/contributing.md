# Contributing

Information about contributing to Lemmy, whether it is translating, testing, designing or programming.

## Issue tracking / Repositories

- [GitHub (for issues)](https://github.com/LemmyNet/lemmy)
- [Gitea](https://yerbamate.dev/LemmyNet/lemmy)
- [GitLab](https://gitlab.com/dessalines/lemmy)

## Translating

Check out [Lemmy's Weblate](https://weblate.yerbamate.dev/projects/lemmy/) for translations.


## Architecture

### Front end

- The front end is written in `typescript`, using a react-like framework called [inferno](https://infernojs.org/). All UI elements are reusable `.tsx` components.
- The main page and routing are in `ui/src/index.tsx`.
- The components are located in `ui/src/components`.

### Back end

- The back end is written in `rust`, using `diesel`, and `actix`.
- The server source code is split into main sections in `server/src`. These include: 
  - `db` - The low level database actions.
    - Database additions are done using diesel migrations. Run `diesel migration generate xxxxx` to add new things.
  - `api` - The high level user interactions (things like `CreateComment`)
  - `routes` - The server endpoints .
  - `apub` - The activitypub conversions.
  - `websocket` - Creates the websocket server. 

## Linting / Formatting

- Every front and back end commit is automatically formatted then linted using `husky`, and `lint-staged`.
- Rust with `cargo fmt` and `cargo clippy`.
- Typescript with `prettier` and `eslint`.
