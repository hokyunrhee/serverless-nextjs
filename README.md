# Serverless Next.js

[Serverless framework](https://www.serverless.com/)와 [Serverless Next.js Component](https://github.com/serverless-nextjs/serverless-next.js#motivation)을 이용하여 Next.js 애플리케이션을 AWS에 배포합니다.

![architecture](https://raw.githubusercontent.com/serverless-nextjs/serverless-next.js/master/img/arch_no_grid.png)

## Getting Started

`serverless.yml` 파일을 생성하고 설정을 추가합니다.

```yml
serverlessNextjs:
  component: "@sls-next/serverless-component@3.7.0"
```

`.env` 파일을 추가하고 AWS credentials를 입력합니다.

```
AWS_ACCESS_KEY_ID=accesskey
AWS_SECRET_ACCESS_KEY=sshhh
```

배포 커맨드를 작성합니다.

```json
  "scripts": {
    "deploy": "serverless"
  }
```

애플리케이션을 배포합니다.

```bash
yarn run deploy
```

## More Configuration

필요에 따라 상세 설정을 할 수 있습니다.

```yml
# serverless.yml

app: serverless-nextjs
stage: ${env.STAGE}
serverlessNextjs:
  component: "@sls-next/serverless-component@3.7"
  inputs:
    cloudfront:
      distributionId: ${env.DISTRIBUTION_ID}
    bucketRegion: ap-northeast-2
    bucketName: "${app}-${stage}-bucket"
    name:
      defaultLambda: "${app}-${stage}-ssr-lambda"
      apiLambda: "${app}-${stage}-api-lambda"
      imageLambda: "${app}-${stage}-image-lambda"
```

## Deploy

최신 serverless 버전은 Serverless Components CLI를 지원하지 않기 때문에 특정 버전을 사용해야 합니다.

```
npx serverless@2.72.2
```

`.serverless`로 시작하는 폴더를 `.gitignore`에 추가합니다.

```
# .gitignore

# Serverless directories
.serverless*
```

## FAQ

몇 가지 궁금한 점들이 있었는데 document에서 확인할 수 있었습니다. FAQ가 잘 되어있는 프로젝트라고 생각합니다.

- [My lambda is deployed to us-east-1. How can I deploy it to another region?](https://github.com/serverless-nextjs/serverless-next.js#my-lambda-is-deployed-to-us-east-1-how-can-i-deploy-it-to-another-region)

- [[CI/CD] Multi-stage deployments / A new CloudFront distribution is created on every CI build. I wasn't expecting that](https://github.com/serverless-nextjs/serverless-next.js#cicd-multi-stage-deployments--a-new-cloudfront-distribution-is-created-on-every-ci-build-i-wasnt-expecting-that)

- [Concatenating environment variables doesn't seem to work](https://github.com/serverless-nextjs/serverless-next.js#concatenating-environment-variables-doesnt-seem-to-work)

- deploy가 실패합니다.  
  "Serverless Components CLI v1 is no longer bundled with Serverless Framework CLI"라는 메시지와 함께 배포 실패가 났습니다. 특정 버전을 이용하여 해결할 수 있었습니다. @2.72.2

## Conclusion

개인적으로 Amplify만큼 편리하다고 느껴집니다. 계속 사용한다면 Amplify보다 나을 것 같습니다. 스타트업이라면 production에 사용할 수도 있을 것 같습니다. 유튜버 [codedamn](https://www.youtube.com/c/codedamn)의 [교육 사이트](https://codedamn.com)가 Serverless Nextjs를 이용하고 있다고 합니다. 작년 연말 [영상](https://www.youtube.com/watch?v=Am6xpAqU27g)에서 이야기했으니까 지금은 아닐 수도 있겠네요.

이 레딧 [코멘트](https://www.reddit.com/r/nextjs/comments/smx6nu/comment/hw4egn4/?utm_source=share&utm_medium=web2x&context=3)에 따르면 Amplify가 Serverless Nextjs를 이용하고 있다고 합니다. 시간이 되면 확인해봐야겠습니다.

장점

- 손쉽게 serverless architecture로 Next.js 애플리케이션을 만들 수 있습니다.
- Next.js 12에 새롭게 추가된 기능들을 제외하고 대부분의 기능이 지원됩니다. 이 부분은 Amplify도 마찬가지입니다.
- yml 파일에 인프라를 정의했기 때문에 재현이 쉽습니다.
- 비교적 쉽게 세부 설정들을 할 수 있습니다.

단점

- 어느 정도 학습이 필요합니다.
- 설정에 일부 버그가 있습니다. 주의가 필요합니다.

<br/>

**예산에 여유가 있다면 DX가 좋은 vercel을 이용하는 것이 좋다고 생각합니다.**
