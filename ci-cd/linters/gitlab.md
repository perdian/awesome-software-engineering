# Linter integrations in GitLab pipelines

## eslint

```yaml
lint-js:
  image: registry.gitlab.com/pipeline-components/eslint:latest
  stage: verify
  script: |-
    eslint $( [[ -e .eslintrc ]] || echo '--no-eslintrc' ) --env es2024 'src/**/*.js'
```

.eslintrc.json in project root:

```json
{
  "extends": "eslint:recommended"
}
```

## yamllint

```yaml
lint-yaml:
  image: registry.gitlab.com/pipeline-components/yamllint:latest
  stage: verify
  script: |-
    pip install yamllint-junit
    yamllint -f parsable . | yamllint-junit -o yamllint-junit.xml
  artifacts:
    reports:
      junit: yamllint-junit.xml
```

## markdownlint-cli2

```yaml
lint-markdown:
  image: registry.gitlab.com/pipeline-components/markdownlint-cli2:latest
  stage: verify
  script: |-
    echo { \"outputFormatters\": [ [ \"markdownlint-cli2-formatter-junit\" ] ]} > .markdownlint-cli2.jsonc
    markdownlint-cli2 "**/*.{md,markdown}"
  artifacts:
    reports:
      junit: markdownlint-cli2-junit.xml
```

## stylelint

```yaml
lint-css:
  image: registry.gitlab.com/pipeline-components/stylelint:latest
  stage: verify
  script: |-
    stylelint --color 'src/**/*.css'
```

.stylelintrc.json in project root:

```json
{
  "extends": "stylelint-config-standard",
  "rules": {
    "color-hex-length": null,
    "declaration-block-single-line-max-declarations": null,
    "media-feature-range-notation": null,
    "no-descending-specificity": null,
    "no-empty-source": null,
    "shorthand-property-no-redundant-values": null
  }
}
```

## xmllint

```yaml
xmllint:
  stage: verify
  image: registry.gitlab.com/pipeline-components/xmllint:latest
  script:
    - find src/ -iname "*.xml" -type f -exec xmllint --noout {} \+
```
