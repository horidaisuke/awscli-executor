# awscli-executor
Circleci executor installed aws cli

## Usage

Define executor in `.circleci/config.yml` like this:

```yaml
executors:
  awscli-executor:
    docker:
      - image: horidaisuke/awscli-executor:latest
    shell: /bin/bash -leo pipefail
    environment:
      - BASH_ENV: /etc/profile

# Use orbs command directly in awscli-executor executor
orbs:
  aws-ecr: circleci/aws-ecr@6.12.2
jobs:
  docker-push-example:
    executor:
      name: awscli-executor
    steps:
      - run:
          command: |
            echo 'export AWS_ECR_ACCOUNT_URL="${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"' >> $BASH_ENV
            echo 'export AWS_REGION="${AWS_DEFAULT_REGION}"' >> $BASH_ENV
      - aws-ecr/ecr-login
      - aws-ecr/push-image:
          repo: example
```

## Tags

* `19.03.13-cli-2.0.54`, `latest`

## License

View [license information](https://github.com/horidaisuke/awscli-executor/blob/main/LICENSE) for the software contained in this image.

This license is inherited from licenses of two docker images, [library/docker](https://hub.docker.com/_/docker) and [amazon/aws-cli](https://hub.docker.com/r/amazon/aws-cli).
