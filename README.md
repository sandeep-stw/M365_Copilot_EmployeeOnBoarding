# Employee Onboarding Assistant — Microsoft 365 Copilot Declarative Agent

A declarative agent for Microsoft 365 Copilot that helps new employees get up to speed quickly. It answers questions about onboarding checklists, company policies, benefits, IT setup, required training, and key contacts — grounded in your organization's own content.

## What it does

- **Onboarding guidance** — first day / first week / 30-60-90 day checklists
- **Policy Q&A** — leave, remote work, expenses, code of conduct
- **Benefits help** — enrollment steps and deadlines
- **IT setup** — accounts, devices, software, VPN, MFA
- **Training** — mandatory compliance courses and deadlines
- **Contacts** — who to reach for HR, IT, payroll, and facilities

## Knowledge sources

The agent grounds its answers in these Microsoft 365 capabilities (configured in [`appPackage/declarativeAgent.json`](./appPackage/declarativeAgent.json)):

| Capability | Purpose |
|---|---|
| `OneDriveAndSharePoint` | HR handbooks, policy documents, onboarding guides |
| `GraphConnectors` | External content indexed via Microsoft Graph connectors |
| `TeamsMessages` | Relevant discussions in Teams channels and chats |
| `Email` | Onboarding emails and announcements |

> **Tip:** To scope SharePoint grounding to specific sites or files, add `items_by_url` to the `OneDriveAndSharePoint` capability. Similarly, `GraphConnectors` supports a `connections` list, and `TeamsMessages` supports `urls`.

## Project structure

```
├── appPackage/
│   ├── manifest.json           # Microsoft 365 app manifest
│   ├── declarativeAgent.json   # Agent definition (name, capabilities, starters)
│   ├── instruction.txt         # Agent instructions (behavior, tone, boundaries)
│   ├── color.png               # 192×192 color icon
│   └── outline.png             # 32×32 outline icon
├── env/
│   └── .env.dev                # Environment variables for the dev environment
├── m365agents.yml              # Microsoft 365 Agents Toolkit project file
└── .vscode/                    # Debug/launch configuration
```

## Prerequisites

- A [Microsoft 365 account](https://developer.microsoft.com/microsoft-365/dev-program) with Microsoft 365 Copilot enabled
- [Custom app upload](https://learn.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading) enabled in your tenant
- [Visual Studio Code](https://code.visualstudio.com/) with the [Microsoft 365 Agents Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) extension, **or** the [Agents Toolkit CLI](https://aka.ms/teamsfx-cli) (`npm install -g @microsoft/m365agentstoolkit-cli`)

## Run and test

### With VS Code (Agents Toolkit extension)

1. Open this folder in VS Code.
2. Sign in to your Microsoft 365 account in the Agents Toolkit extension.
3. Press **F5** (or select **Preview in Copilot (Edge)** from the Run and Debug panel).
4. In Microsoft 365 Copilot chat, select the **Employee Onboarding** agent from the agent list and start chatting.

### With the CLI

```bash
# Provision (registers the app and sideloads it to your tenant)
atk provision --env dev

# Preview in Copilot
atk preview --env dev
```

## Publish to your organization

```bash
atk publish --env dev
```

This submits the app package to the Teams Admin Center, where an admin can review and approve it for the whole organization.

## Customizing

- **Instructions** — edit [`appPackage/instruction.txt`](./appPackage/instruction.txt) (max 8,000 characters).
- **Conversation starters** — edit the `conversation_starters` array in [`appPackage/declarativeAgent.json`](./appPackage/declarativeAgent.json).
- **Name/description/icons** — edit [`appPackage/manifest.json`](./appPackage/manifest.json) and replace the PNG icons.

## Learn more

- [Declarative agents for Microsoft 365 Copilot](https://learn.microsoft.com/microsoft-365-copilot/extensibility/overview-declarative-agent)
- [Declarative agent schema reference (v1.5)](https://learn.microsoft.com/microsoft-365-copilot/extensibility/declarative-agent-manifest-1.5)
- [Microsoft 365 Agents Toolkit](https://learn.microsoft.com/microsoft-365-copilot/extensibility/agents-toolkit)
