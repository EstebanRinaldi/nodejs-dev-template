# NodeJS Developer Environment Template

Template for NodeJS development with VSCode inside a Docker Container.

## Requirements

- [Visual Studio Code](https://code.visualstudio.com/)
- [VS Code Remote Development Extension](https://aka.ms/vscode-remote/download/extension)
- [VS Code Docker Extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) *(optional)*

## Usage

1. Clone the repo.
2. Update the .env file.
3. Run the **Remote-Containers: Reopen in Container...** command from the Command Palette (F1) or quick actions Status bar item.
4. Optionally update the package.json to match your project.
5. Start working.

To return to the local project:
- Run the **Remote-Containers: Reopen Locally...** command from the Command Palette (F1) or quick actions Status bar item.

## Development Container

The container includes NodeJS (ckech .env to change version), with nodemon and Yarn installed globally.

### VS Code Extensions

- "dbaeumer.vscode-eslint",
- "mtxr.sqltools",
- "mtxr.sqltools-driver-pg",
- "mtxr.sqltools-driver-mysql",
- "mtxr.sqltools-driver-mssql",
- "ms-mssql.mssql",
- "mikestead.dotenv",
- "CoenraadS.bracket-pair-colorizer-2",
- "aaron-bond.better-comments",
- "christian-kohler.path-intellisense",
- "yzhang.markdown-all-in-one",
- "bierner.markdown-preview-github-styles",
- "EditorConfig.EditorConfig",
- "oouo-diogo-perdigao.docthis",
- "Orta.vscode-jest",
- "rangav.vscode-thunder-client",
- "xabikos.javascriptsnippets",
- "esbenp.prettier-vscode",
- "wallabyjs.quokka-vscode",
- "eamodio.gitlens",
- "gamunu.vscode-yarn",
- "hediet.vscode-drawio"

### NodeJS Project

The project includes eslint (airbnb config), prettier and jest as development dependencies.

## Docker Services Included

- MSSQL
- Postgres (with pgAdmin)
- MySQL (with phpMyAdmin)
- MariaDB (with phpMyAdmin)

## External Links

- [Developing inside a Container](https://code.visualstudio.com/docs/remote/containers)
