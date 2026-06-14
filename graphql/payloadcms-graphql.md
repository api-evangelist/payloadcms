# Payload CMS GraphQL API

Payload CMS ships a fully featured GraphQL API generated automatically from your collection and global configurations. Every collection defined in your Payload config produces a set of strongly-typed queries and mutations — find by ID, find (paginated), count, create, update, delete, duplicate, and version operations — all derived from the collection slug and its field definitions. Auth-enabled collections additionally receive login, logout, refresh, me, forgotPassword, resetPassword, verifyEmail, unlock, and initialized operations. Globals receive a findOne query and an update mutation. The schema is built at startup using `@payloadcms/graphql`'s `configToSchema()` function, and the resulting SDL can be exported with `pnpm payload-graphql generate:schema`.

Authentication is handled via the `login{CollectionSingular}` mutation, which returns a JWT token. That token is passed as a `Bearer` token in the `Authorization` header of subsequent requests (`Authorization: Bearer <token>`). The API also supports cookie-based auth when accessed through a browser session. Complexity limiting is built in (configurable via `graphQL.maxComplexity` in the Payload config), and introspection is disabled in production by default. A GraphQL Playground is available at `/api/graphql-playground` during development. Because the schema is dynamic and generated from user-defined collections, the exact types available will vary per deployment. The built-in types documented here reflect the framework's generated patterns and the standard built-in collections (`users`, `payload-preferences`).

Localization is optionally supported: if a Payload config enables localization, all queries gain `locale` (a `LocaleInputType` enum of configured locale codes) and `fallbackLocale` (a `FallbackLocaleInputType` enum including `none`) arguments. Versioning support adds `version{Singular}` and `versions{Plural}` queries, and a `restoreVersion{Singular}` mutation. Draft support adds a `draft` boolean argument to queries and mutations. The schema pattern for each collection follows a consistent naming convention: singular PascalCase names for single-document operations and plural names for list operations, derived from the collection slug after word-formatting and special-character removal.

**Endpoint:** `https://{your-domain}/api/graphql`

**Playground:** `https://{your-domain}/api/graphql-playground` (development only by default)

**Documentation:** https://payloadcms.com/docs/graphql/overview

**References:**
- Documentation: https://payloadcms.com/docs/graphql/overview
- Schema Generation: https://payloadcms.com/docs/graphql/graphql-schema
- Extending GraphQL: https://payloadcms.com/docs/graphql/extending
- GettingStarted: https://payloadcms.com/docs/getting-started/what-is-payload
- GitHub Source (schema builders): https://github.com/payloadcms/payload/tree/main/packages/graphql/src/schema
- GitHub Source (resolvers): https://github.com/payloadcms/payload/tree/main/packages/graphql/src/resolvers
