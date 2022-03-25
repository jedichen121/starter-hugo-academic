# [Hugo Academic Theme](https://github.com/wowchemy/starter-hugo-academic)

[![Screenshot](https://raw.githubusercontent.com/wowchemy/wowchemy-hugo-themes/main/academic.png)](https://wowchemy.com/hugo-themes/)

The Hugo **Academic Resumé Template** empowers you to easily create your job-winning online resumé, showcase your academic publications, and create online courses or knowledge bases to grow your audience.



# Setup tutorial

## Install Hugo

Follow the installation guide [here](https://gohugo.io/getting-started/installing/). 

For Linux, it's recommended to download pre-build binaries. Using `apt` and `snap` might incur unexpected errors. 

## Build website

To build the website, you can use
```
hugo
```
then it will generate the website and place all files in the `public/` directory. 

To view changes to the website live, use 
```
hugo server
```

and the website will be available at http://localhost:1313. In this mode Hugo will automatically re-generate your site whenever you change your sources.

## Automatic build with Github Action

### Create Github token

Follow this [guide](https://ruddra.com/hugo-deploy-static-page-using-github-actions/) to create a personal token and add it as a secret to this project. 

### Create a Github action

Create a file in `.github/workflows/gh-pages.yml` (you might need to create the folder as well) and add the following content. 

```
name: github pages

on:
  push:
    branches:
      - master  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.95.0'
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/master'
        with:
          github_token: ${{ secrets.TOKEN }}
          publish_dir: ./public
```


Make sure to replace `master` with your source code's branch. It's also important that the `secrets.TOKEN` has the same name as the secret you created. 

For more detailed explaination of each field please check this [guide](https://lakemper.eu/blog/getting-started-with-hugo-academic-and-github-pages/).


Remember to change the `baseURL` in `config.yaml` to your website address, such as `https://<USERNAME|ORGANIZATION>.github.io/`.
## Website customization

Please follow the guide [here](https://wowchemy.com/docs/getting-started/customization/).



## Use Custom domain

### Apply for a domain

You can apply for a domain in website like https://domains.google/ or https://www.godaddy.com/.

### Verify domain with Github

Follow this [guide](https://thecesrom.dev/2020/10/14/how-to-verify-your-github-organization-s-domain-on-google-domains/) for verifying the domain with Github. It might take a day.

### Set up custom domain for the repository

Follow this [guide](https://dev.to/trentyang/how-to-setup-google-domain-for-github-pages-1p58) for how to setup Google domain with github pages.

After it's done, don't forget to change the `baseURL` to the new domain address. 