# Deploy templates

You can deploy templates that generate the initial configuration for your project, including the first commit on versionable subsystems. Deploying templates may require access to GitHub in order to create a repository and push the initial source files.

To authorize GitHub in CED

```bash
$ ced int:github
```

To deploy a template

```bash
$ ced template:deploy <template-filename>
```

Some sample templates can be found [here](../../libs//internal/templates/ced-templates-test/test-templates/).
