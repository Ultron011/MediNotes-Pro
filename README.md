This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/pages/api-reference/create-next-app).

## Getting Started

### Environment Variables

This project requires Clerk authentication keys. You need to set up the following environment variables:

1. **Get your Clerk keys:**
   - Visit [Clerk Dashboard](https://dashboard.clerk.com/last-active?path=api-keys)
   - Copy your **Publishable Key** (starts with `pk_test_` or `pk_live_`)
   - Copy your **JWKS URL** (found in your Clerk instance settings)

2. **For local development, create a `.env.local` file:**
   ```bash
   NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_your_key_here
   CLERK_JWKS_URL=https://your-clerk-instance.clerk.accounts.dev/.well-known/jwks.json
   ```

3. **For production builds:**
   - Local build: Ensure `.env.local` exists with `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`
   - Docker build: Pass the key as a build argument (see Docker section below)

### Development

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.tsx`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/pages/building-your-application/routing/api-routes) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.ts`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/pages/building-your-application/routing/api-routes) instead of React pages.

This project uses [`next/font`](https://nextjs.org/docs/pages/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn-pages-router) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Building for Production

### Local Build

Make sure you have a `.env.local` file with `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` set:

```bash
npm run build
```

### Docker Build

#### Option 1: Using Docker Compose (Recommended)

1. Create a `.env` file in the project root with your credentials:

```bash
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_your_key_here
CLERK_JWKS_URL=https://your-clerk-instance.clerk.accounts.dev/.well-known/jwks.json
OPENAI_API_KEY=sk-your-openai-api-key-here
```

2. Build and run with Docker Compose:

```bash
docker-compose up --build
```

The app will be available at `http://localhost:8000`

#### Option 2: Manual Docker Build

Build the Docker image with the Clerk publishable key:

```bash
docker build --build-arg NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_your_key_here -t saas-app .
```

Run the container:

```bash
docker run -p 8000:8000 \
  -e CLERK_JWKS_URL=https://your-clerk-instance.clerk.accounts.dev/.well-known/jwks.json \
  -e OPENAI_API_KEY=sk-your-openai-api-key-here \
  saas-app
```

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/pages/building-your-application/deploying) for more details.
