# Jaks.TS

A minimalistic Nuxt Jamstack starter template using TypeScript, Vuetify, and API Repository Pattern. JAKS!

&nbsp;

## Installation

```
npm install
```

> Run **Locally**

```
npm run dev
```
 
> Generate **Static** Pages

```
npm run build:static
```

```
cd dist/
```

```
npx serve
```

&nbsp;

## Contributing

Made with ❤️ at [Nuxify](https://nuxify.tech)

&nbsp;

## License

[MIT](https://choosealicense.com/licenses/mit/)

## Learning

- Afther executing build file, you can test the dist folder by typing:
  ```
    serve -s dist
  ```
- Nuxt is a framework for vue. But much efficient and faster. SEO optimization. 
- Nuxt has control of head, title, meta, etc.
- Simple page routing because of the page folder, we can simply go to the specific route that match our file
- Choice between Universal or SPA
- We can also include UI Framework such as Boostrap.


## To deploy nuxt into github pages
- [Nuxt Documentation](https://nuxtjs.org/deployments/github-pages/), [Github Action (Automation)](https://docs.github.com/en/actions), [Adding Secret To Repository](https://github.com/Azure/actions-workflow-samples/blob/master/assets/create-secrets-for-GitHub-workflows.md)
  - Semi Manual:
    - First Setup nux.config.js:
      ```
        export default {
          ...,
          target: 'static',
          router:{
            base:'/jaksnuxtsort/' /* Name of github repo */
          },
          ...,
        }
      ```
    - install package for pushing directory directly:
      ```
        npm install push-dir --save-dev

      ```
    - In your package.json add this inside script:
      ```
        ...,
        "deploy": "push-dir --dir=dist --branch=gh-pages --cleanup"
        ...,
      ```
    - npm run generate
    - npm run deploy this will deploy the generated dist folder directly to your gh-page branch

  - Build server deployment
    - Create a Github Action to the repo or simple create on terminal:
      ```
      $~ mkdir .github
      $~ mkdir workflow
      $~ touch cd.yml
      ```
    - In your cd.yml:
      ```
      name: cd

      on: [push, pull_request]

      jobs:
        cd:
          runs-on: ${{ matrix.os }}

          strategy:
            matrix:
              os: [ubuntu-latest]
              node: [14]
        

          steps:
            - name: Checkout
              uses: actions/checkout@master

            - name: Setup node env
              uses: actions/setup-node@v2.1.2
              with:
                node-version: ${{ matrix.node }} # this is from strategy above

            - name: Install dependencies
              run: npm

            - name: Generate
              run: npm generate
          

            - name: Deploy
              uses: peaceiris/actions-gh-pages@v3
              with:
                github_token: ${{ secrets.GITHUBTOKEN }} # this is from github repo settings > secret you can simply create using the referece above
                publish_dir: ./dist
      ```
    - Then simply commit and push changes:
      ```
        git add .github/workflows/cd.yml
        git commit -m "Adding github pages deploy workflow"
        git push origin
      ```
    - Visit [Jaks Template Try](https://josephgcedeno.github.io/jaksnuxtsort/)

