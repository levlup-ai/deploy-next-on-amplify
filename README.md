This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.js`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/api-routes/introduction) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.js`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/api-routes/introduction) instead of React pages.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on AWS Amplify

To launch a Next.js app online, you need to deploy it. AWS Amplify is a cost-effective and ready-for-scale option, which supports deploying both SSR and SSG Next.js apps without any additional configuration.

If you're creating a statically generated Next.js app, go to your `package.json` file and change your build script from `next build` to `next build && next export`. If you're instead creating a server-side rendered app, you don't need to change a thing! The scripts Next.js generated for you will be what you need.

```
"scripts": {
  "dev": "next dev",
  "build": "next build [ + optional: && next export]",
  "start": "next start"
},
```

Then, create a repository on your git provider of choice, and push your code to it.

### Deployment

1. Create an AWS account if you don't already have one.
2. Navigate to the Amplify Console
3. Click on the orange `connect app` button _─If you already have apps, you'll need to click `new app`, then `Host Web App`_
4. Choose your git provider of choice (in my case Github) in the `From your existing code` menu, and click continue
   [!alt text](https://welearncode.com/beginners-guide-react-2020/choose-github.png)
5. Type in the name of your GitHub repo you just created (it should autofill!) and then click `next`
   [!alt text](https://welearncode.com/beginners-guide-react-2020/select-your-repo.png)
6. The build settings will auto-populate, and so you can just click `next` on the `Configure build settings` _(Note: If you are deploying an SSR or hybrid app, you may need to read point 8 below)_
7. **[Optional -But IMPORTANT for SSR APPS!]** If your frontend requires backend-access permission, you will be asked to [select an existing service role](https://aws.amazon.com/blogs/mobile/host-a-next-js-ssr-app-with-real-time-data-on-aws-amplify/) or [create a new one](https://docs.aws.amazon.com/amplify/latest/userguide/how-to-service-role-amplify-console.html), so that Amplify Console may access your resources: if you don't already have a service role, click `create new role`, which will open up an `IAM` role management window. There, leave all as default but make sure that under `Attached permissions policies` you have both `AdministratorAccess-Amplify` and `AdministratorAccess`: if you don't add the missing one(s).
8. Click `Save and deploy`.
