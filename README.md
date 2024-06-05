# Fiori Template File for any other SAPUI5 Project


## Changes


### Deployment

#### Credentials

> Register credential for easier deployment

- ADD a `.env` file in root directory
```
CFT_USERNAME=
CFT_PASSWORD=
```

- ADD the following code under `customerTasks->name->configuration` in file `ui5-deploy.yaml`

```
  customTasks:
    - name: deploy-to-abap
      afterTask: generateCachebusterInfo
      configuration:
        target:
          destination: xx
          url: http://cft.xxxx.xx:xxxx
        credentials:
          username: env:CFT_USERNAME
          password: env:CFT_PASSWORD
```

#### Auto Deployment on commit

> Make a deployment on every `commit`. \
> Based on the principle that every commit should be working.

- Add a new script in `package.json`
```
"noconfirm-deploy": "npm run build && fiori deploy -y --config ui5-deploy.yaml && rimraf archive.zip",
```

- Create a file `post-commit` under `.git/hooks/`
- Add your deployment command (`npm run noconfirm-deploy`)
- Add execution right to file (`chmod +x .git/hooks/post-commit`)
