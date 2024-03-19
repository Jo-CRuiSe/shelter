# Unpublished Posts Enhancement for Chirpy Theme

[![Gem Version](https://img.shields.io/gem/v/jekyll-theme-chirpy-customized-upe)][gem]&nbsp;
[![GitHub license](https://img.shields.io/github/license/cotes2020/chirpy-starter.svg?color=blue)][mit]

*Derived from [Chirpy][chirpy] theme*

[中文版](https://github.com/Jo-CRuiSe/jekyll-theme-chirpy-customized-upe/blob/master/README%20(CN).md)

## Why do I need this customization?

While using the Chirpy theme, I have noticed some functionalities that are different from what I'm accustomed to and some functionalities that are still missing. These include implementing blog login access (the current repository should be set to private or deployed to my own server), enhancing the Mathjax plugin, and changing the UI style, among others. Additionally, this serves as a challenge to test my frontend coding skills.

> The next steps are similar to the Chirpy documentation

## Installation

### Creating a New URL

Sign in to GitHub and browse to [**unpublished-posts-enhancement**](https://github.com/Jo-CRuiSe/unpublished-posts-enhancement), click the button <kbd>[Use this template][use-template]</kbd> > <kbd>Create a new repository</kbd>, and name the new repository to what you like which represents your unpulished posts pages URL.

### Installing Dependencies

Before running local server for the first time, go to the root directory of your site and run:

```console
$ bundle
```

## Usage

You may want to preview the site contents before publishing, so just run it by:

```console
$ bundle exec jekyll s
```

After a few seconds, the local service will be published at _<http://127.0.0.1:4000>_.

## Deployment

Before the deployment begins, check out the file `_config.yml`and make sure the `url` is configured correctly. Remember to change the `baseurl` to your project name that starts with a slash, e.g, `/project-name`.

Now you can choose _ONE_ of the following methods to deploy your Jekyll site.

### Deploy by Using GitHub Actions

There are a few things to get ready for.

- If you're on the GitHub Free plan, keep your site repository public.
- If you have committed `Gemfile.lock` to the repository, and your local machine is not running Linux, go to the root of your site and update the platform list of the lock-file:

  ```console
  $ bundle lock --add-platform x86_64-linux
  ```

Next, configure the _Pages_ service.

1. Browse to your repository on GitHub. Select the tab _Settings_, then click _Pages_ in the left navigation bar. Then, in the **Source** section (under _Build and deployment_), select [**GitHub Actions**][pages-workflow-src] from the dropdown menu.  

2. Push any commits to GitHub to trigger the _Actions_ workflow. In the _Actions_ tab of your repository, you should see the workflow _Build and Deploy_ running. Once the build is complete and successful, the site will be deployed automatically.

At this point, you can go to the URL indicated by GitHub to access your site.

### Manually Build and Deploy

On self-hosted servers, you cannot enjoy the convenience of **GitHub Actions**. Therefore, you should build the site on your local machine and then upload the site files to the server.

Go to the root of the source project, and build your site as follows:

```console
$ JEKYLL_ENV=production bundle exec jekyll b
```

Unless you specified the output path, the generated site files will be placed in folder `_site`of the project's root directory. Now you should upload those files to the target server.

## Configuration

[This blog](https://jo-cruise.github.io/2024-02-06-HowToUseUPE) will guide you to complete relative configuration.


## License

This work is published under [MIT][mit] License.

[gem]: https://rubygems.org/gems/jekyll-theme-chirpy-customized-upe
[chirpy]: https://github.com/cotes2020/jekyll-theme-chirpy/
[use-template]: https://github.com/Jo-CRuiSe/unpublished-posts-enhancement/generate
[CD]: https://en.wikipedia.org/wiki/Continuous_deployment
[mit]: https://github.com/Jo-CRuiSe/jekyll-theme-chirpy-customized-upe/blob/master/LICENSE
