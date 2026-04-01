# boneyard

Pixel-perfect skeleton loading screens, extracted from your real DOM.

## Quick start

```bash
npm install boneyard-js
```

```tsx
import { Skeleton } from 'boneyard-js/react'

<Skeleton name="blog-card" loading={isLoading}>
  <BlogCard data={data} />
</Skeleton>
```

```bash
npx boneyard-js build
```

```tsx
// app/layout.tsx
import './bones/registry'
```

Done. See the [full documentation](https://github.com/0xGF/boneyard) for all props, CLI options, and examples.

## License

MIT
