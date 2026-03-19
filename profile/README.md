# Oxy

Building the identity and app platform for the next generation of connected services.

## Ecosystem

| App | Description | Stack |
|-----|-------------|-------|
| [**OxyHQServices**](https://github.com/OxyHQ/OxyHQServices) | Platform monorepo — identity, auth SDK, API, email | TypeScript, Express, Expo |
| [**Mention**](https://github.com/OxyHQ/Mention) | People-first social network | React Native, Expo |
| [**Allo**](https://github.com/OxyHQ/Allo) | Communication app | React Native, Expo |
| [**Alia**](https://github.com/OxyHQ/Alia) | AI assistant platform | React Native, Expo |
| [**Bloom**](https://github.com/OxyHQ/Bloom) | Cross-platform UI component library | React Native |
| [**Schedio**](https://github.com/OxyHQ/Schedio) | Design and prototyping tool | React Native, Expo |
| [**Homiio**](https://github.com/OxyHQ/Homiio) | Real estate platform | React Native, Expo |
| [**Musico**](https://github.com/OxyHQ/Musico) | Music platform | React Native, Expo |
| [**Athina**](https://github.com/OxyHQ/Athina) | Legal justice documentation platform | TypeScript, Payload CMS |
| [**Codea Studio**](https://github.com/OxyHQ/CodeaStudioCode) | AI-powered code editor | TypeScript, VS Code |
| [**OxyOS**](https://github.com/OxyHQ/OxyOS) | Desktop operating system | Linux |

## SDK

All Oxy apps share a common identity and auth layer:

```
@oxyhq/core      — Platform-agnostic foundation (auth, crypto, API client)
@oxyhq/auth      — Web auth SDK (React hooks, FedCM SSO)
@oxyhq/services  — React Native / Expo SDK (UI, screens, native features)
```

## For Developers

- [Engineering Standards](https://github.com/OxyHQ/engineering) — Code quality, conventions, and developer setup
- [Contributing Guide](https://github.com/OxyHQ/.github/blob/main/CONTRIBUTING.md)
- [Security Policy](https://github.com/OxyHQ/.github/blob/main/SECURITY.md)
- [Documentation](https://github.com/OxyHQ/OxyHQServices/wiki)
- [Project Board](https://github.com/orgs/OxyHQ/projects/14)

## Links

- [oxy.so](https://oxy.so)

## License

MIT
