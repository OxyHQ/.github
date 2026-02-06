# Oxy

Building the identity and app platform for the next generation of connected services.

## Ecosystem

| App | Description | Stack |
|-----|-------------|-------|
| [**OxyHQServices**](https://github.com/OxyHQ/OxyHQServices) | Platform monorepo — identity, auth SDK, API, email | TypeScript, Express, Expo |
| [**Mention**](https://github.com/OxyHQ/Mention) | People-first social network | React Native, Expo |
| [**Allo**](https://github.com/OxyHQ/Allo) | Communication app | React Native, Expo |
| [**Homiio**](https://github.com/OxyHQ/Homiio) | Real estate platform | React Native, Expo |
| [**Musico**](https://github.com/OxyHQ/Musico) | Music platform | React Native, Expo |
| [**Codea Studio**](https://github.com/OxyHQ/CodeaStudioCode) | AI-powered code editor | TypeScript, VS Code |

## SDK

All Oxy apps share a common identity and auth layer:

```
@oxyhq/core      — Platform-agnostic foundation (auth, crypto, API client)
@oxyhq/auth      — Web auth SDK (React hooks, FedCM SSO)
@oxyhq/services  — React Native / Expo SDK (UI, screens, native features)
```

## Links

- [oxy.so](https://oxy.so)
- [Documentation](https://github.com/OxyHQ/OxyHQServices/wiki)
- [Project Board](https://github.com/orgs/OxyHQ/projects/14)

## License

MIT
