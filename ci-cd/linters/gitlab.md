# Linter integrations in GitLab pipelines

## yamllint

```yaml
lint-yaml:
  image: "registry.gitlab.com/pipeline-components/yamllint:latest"
  stage: "build"
  script: |-
    pip install pip install yamllint-junit
    yamllint -f parsable ./examples/yaml/ | yamllint-junit -o yamllint-junit.xml
  artifacts:
    reports:
      junit: yamllint-junit.xml
```

## markdownlint-cli2

```yaml
lint-markdown:
  image: "registry.gitlab.com/pipeline-components/markdownlint-cli2:latest"
  stage: "build"
  script: |-
    echo { \"outputFormatters\": [ [ \"markdownlint-cli2-formatter-junit\" ] ]} > .markdownlint-cli2.jsonc
    markdownlint-cli2 ./examples/markdown/
  artifacts:
    reports:
      junit: markdownlint-cli2-junit.xml
```
