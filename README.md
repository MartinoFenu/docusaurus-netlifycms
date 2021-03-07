# Docusaurus + Netlify CMS

This project is built using [Docusaurus 2](https://v2.docusaurus.io/), [Netlify CMS](https://www.netlifycms.org/) modern static website generator.

Instead of updating manually the `sidebars.json` file, here we use [docusaurus-plugin-auto-sidebars](https://www.npmjs.com/package/docusaurus-plugin-auto-sidebars) to generate a `sidebars.auto.json` file, please go to the page of the package to see how to customize the generated file.

## Installation

To install all the dependecies run

```console
npm install
```

This repository has a pre-defined `config.yml` used to tell Netlify CMS wich settings to use, you need to set at least the required options to use the CMS, for more information see [Configuration Options](https://www.netlifycms.org/docs/configuration-options/).

### Local Development

To start only the frontend app you can run

```console
npm start
```

If you want to test your Netlify CMS configuration you can use a beta feature and locally run a proxy server, you should configurate the file in `/static/admin/config.yml` with:
```yml
backend:
  name: git-gateway
local_backend: true
```

And run the backend server
```console
npx netlify-cms-proxy-server
```
More informations on [Working with a Local Git Repository](https://www.netlifycms.org/docs/beta-features/#working-with-a-local-git-repository).

Now you can reach your site on `localhost:3000` and the Netlify CMS on `localhost:3000/admin`.

## Using a remote repository and authentication

In the configuration file the configuration to use Github, Bitbucket and Gitlab are present, tested and commented. You can keep the configuration that you need to work with the system of your choice.

To make this work you should first set up an authentication provider with [Use OAuth provider tokens on your site](https://docs.netlify.com/visitor-access/oauth-provider-tokens/#using-an-authentication-provider).
If you want you can instead use **Git-Gateway** for **Gitlab** and **GIthub** repos, [Netlify and Git-Gateway](https://docs.netlify.com/visitor-access/git-gateway/).

### Github

Follow this link for more information on [Netlify CMS and Github](https://www.netlifycms.org/docs/github-backend/).

You can find the basic configuration:
```yml
backend:
  name: github
  repo: repo-path # following git naming owner-name/repo-name
  branch: main # to avoid Failed to persist entry: API_ERROR: Not Found
```

### Bitbucket

The Bitbucket basic configuration requires little effort and you can log in using your bitbucket account.
```yml
backend:
  name: bitbucket
  repo: repo-path # following git naming owner-name/repo-name
```
You can also use [Bitbucket's implicit grant](https://www.netlifycms.org/docs/bitbucket-backend/#client-side-implicit-grant-bitbucket) but you will need to relog after an hour and all not-saved work will be lost.

### Gitlab

Gitlab is not much different from the previous two:
```yml
backend:
  name: gitlab
  repo: owner-name/repo-name 
```
In this case you can use implicit grants from Gitlab, but this method is going to be deprecated.

## Deploy on Netlify

To deploy this app on Netlify you should create a new site, choose the repository and use as build command `npm run build` and as publish directory `build/`.

After this you should create an **Authorization Code Flow with Netlify** based on the platform that you choose (bitbucket, gitlab or github).