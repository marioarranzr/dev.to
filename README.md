[![Build Status](https://travis-ci.org/marioarranzr/dev.to.svg?branch=master)](https://travis-ci.org/marioarranzr/dev.to)

# How to publish a new post

## Create draft dev.to article

Configure you own `config.json` and put it in tools folder:

```json
{
  "apiKey": [DEV_TO_API_KEY],
  "templateFolder": "template-post",
  "targetFolder": [YOUR_PATH_TO_FOLDER_POSTS] // e.g. "Users/mario/dev/dev.to/blog-posts" or "./blog-posts"
}
```

Run

```
./tools/create-post.js "Hello world is my new post"
```

Modify the generated files and once it is merged to `master` branch, it will be pusbished to [dev.to](https://dev.to)

> Thanks to [ramclen](https://github.com/ramclen/documenting-dev) for his `create-post.js` script and [maxime1992](https://github.com/maxime1992/dev.to) for the template

---

## First, what is dev.to?

https://dev.to is a free and open source blogging platform for developers.

> dev.to (or just DEV) is a platform where software developers write articles, take part in discussions, and build their professional profiles. We value supportive and constructive dialogue in the pursuit of great code and career growth for all members. The ecosystem spans from beginner to advanced developers, and all are welcome to find their place within our community.

## Why would I want to put all my blog posts on a git repo?

- Don't be afraid to mess up with one of your articles while editing it
- Same good practices as when you're developing (format, commits, saving history, compare, etc)
- Use prettier to format the markdown and all the code
- Let people contribute to your article by creating a PR against it (tired of comments going sideways because of some typos? Just let people know they can make a PR at the end of your blog post)

## How do I choose which files I want to publish?

There's a `dev-to-git.json` file where you can define an array of blog posts, e.g.

```json
[
  {
    "id": 12345,
    "relativePathToArticle": "./blog-posts/template-post/template-post.md"
  }
]
```

## How can I find the ID of my blog post on dev.to?

This repository is made to **edit** a blog post. Whether it's published or just a draft, you **have to create it** on dev.to directly. Unfortunately, dev.to does not display the ID of the blog post on the page. So once it's created, you can open your browser console and paste the following code to retrieve the blog post ID:  
`$('div[data-article-id]').getAttribute('data-article-id')`

## How do I configure every blog post individually?

A blog post has to have a [**front matter**](https://dev.to/p/editor_guide) header. You can find an example in this repository here: https://github.com/maxime1992/dev.to/blob/master/blog-posts/name-of-your-blog-post/name-of-your-blog-post.md

Simple and from there you have control over the following properties: `title`, `published`, `cover_image`, `description`, `tags`, `series` and `canonical_url`.

## How do I add images to my blog posts?

Instead of uploading them manually on dev.to, simply put them within your git repo and within the blog post use a relative link. Here's an example: `The following is an image: ![alt text](./assets/image.png 'Title image')`.

If you've got some plugin to preview your markdown from your IDE, the images will be correctly displayed. Then, on CI, right before they're published, the link will be updated to match the raw file.

## How to setup CI for auto deploying the blog posts?

If you want to use Github and Travis, a `.travis.yml` file has been already prepared for you.

First, you have to activate the repository on Travis: https://travis-ci.org/account/repositories

Then, you have to create a token on your dev.to account: https://dev.to/settings/account and set an environment variable on Travis called `DEV_TO_GIT_TOKEN` that will have the newly created token as value.
