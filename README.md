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

_Note: If you don't want to give your backend service role full admin access, here is a list of service permissions that should be able to support an SSR deployment:_

If you get this error when building a NextJs SSR application, it's likely that the IAM role associated to your App does not have sufficient permissions to deploy resources in your account. For SSR apps, we deploy things like an S3 bucket, a CloudFront distribution, Lambda@Edge functions, an SQS queue (if using ISR) and IAM roles. The following IAM policy is a recommended baseline of permissions that your role needs, but feel free to adjust it to your needs:

<details>
  <summary>IAM permissions for Amplify App Role</summary>

```
acm:DescribeCertificate
acm:ListCertificates
acm:RequestCertificate
cloudfront:CreateCloudFrontOriginAccessIdentity
cloudfront:CreateDistribution
cloudfront:CreateInvalidation
cloudfront:GetDistribution
cloudfront:GetDistributionConfig
cloudfront:ListCloudFrontOriginAccessIdentities
cloudfront:ListDistributions
cloudfront:ListDistributionsByLambdaFunction
cloudfront:ListDistributionsByWebACLId
cloudfront:ListFieldLevelEncryptionConfigs
cloudfront:ListFieldLevelEncryptionProfiles
cloudfront:ListInvalidations
cloudfront:ListPublicKeys
cloudfront:ListStreamingDistributions
cloudfront:UpdateDistribution
cloudfront:TagResource
cloudfront:UntagResource
cloudfront:ListTagsForResource
iam:AttachRolePolicy
iam:CreateRole
iam:CreateServiceLinkedRole
iam:GetRole
iam:PutRolePolicy
iam:PassRole
lambda:CreateFunction
lambda:EnableReplication
lambda:DeleteFunction
lambda:GetFunction
lambda:GetFunctionConfiguration
lambda:PublishVersion
lambda:UpdateFunctionCode
lambda:UpdateFunctionConfiguration
lambda:ListTags
lambda:TagResource
lambda:UntagResource
route53:ChangeResourceRecordSets
route53:ListHostedZonesByName
route53:ListResourceRecordSets
s3:CreateBucket
s3:GetAccelerateConfiguration
s3:GetObject
s3:ListBucket
s3:PutAccelerateConfiguration
s3:PutBucketPolicy
s3:PutObject
s3:PutBucketTagging
s3:GetBucketTagging
lambda:ListEventSourceMappings
lambda:CreateEventSourceMapping
iam:UpdateAssumeRolePolicy
iam:DeleteRolePolicy
sqs:CreateQueue           // SQS only needed if using ISR feature
sqs:DeleteQueue
sqs:GetQueueAttributes
sqs:SetQueueAttributes
amplify:GetApp
amplify:GetBranch
amplify:UpdateApp
amplify:UpdateBranch
```

</details>
