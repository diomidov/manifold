# Installing
1. `yarn install` 
2. `yarn start`
3. `Y` to `Set up and develop “~path/to/the/repo/manifold”? [Y/n]`
4. `Manifold Markets` to `Which scope should contain your project? [Y/n] `
5. `Y` to `Link to existing project? [Y/n] `
6. `opengraph-image` to `What’s the name of your existing project?` 
  
# Quickstart

1. To test locally: `yarn start`
   The local image preview is broken for some reason; but the service works.
   E.g. try `http://localhost:3000/manifold.png`
2. To deploy: push to Github
- note: (Not `dev` because that's reserved for Vercel)
- note2: (Or `cd .. && vercel --prod`, I think)

For more info, see Contributing.md  
(Everything below is from the original repo)

# Development
- Code of interest is contained in the `api/_lib` directory, i.e. `template.ts` is the page that renders the UI.
- Edit `parseRequest(req: IncomingMessage)` in `parser.ts` to add/edit query parameters.
- Note: When testing a remote branch on vercel, the og-image previews that apps load will point to 
`https://manifold-og-image.vercel.app/m.png?question=etc.`, (see relevant code in `SEO.tsx`) and not your remote branch.
You have to find your opengraph-image branch's url and replace the part before `m.png` with it.
  - You can also preview the image locally, e.g. `http://localhost:3000/m.png?question=etc.`
  - Every time you change the template code you'll have to change the query parameter slightly as the image will likely be cached.
- You can find your remote branch's opengraph-image url by click `Visit Preview` on Github:
![](../../../../../Desktop/Screen Shot 2022-08-01 at 2.56.42 PM.png)


# [Open Graph Image as a Service](https://og-image.vercel.app)

<a href="https://twitter.com/vercel">
    <img align="right" src="https://og-image.vercel.app/tweet.png" height="300" />
</a>

Serverless service that generates dynamic Open Graph images that you can embed in your `<meta>` tags.

For each keystroke, headless chromium is used to render an HTML page and take a screenshot of the result which gets cached.

See the image embedded in the tweet for a real use case.

## What is an Open Graph Image?

Have you ever posted a hyperlink to Twitter, Facebook, or Slack and seen an image popup?
How did your social network know how to "unfurl" the URL and get an image?
The answer is in your `<head>`.

The [Open Graph protocol](http://ogp.me) says you can put a `<meta>` tag in the `<head>` of a webpage to define this image.

It looks like the following:

```html
<head>
  <title>Title</title>
  <meta property="og:image" content="http://example.com/logo.jpg" />
</head>
```

## Why use this service?

The short answer is that it would take a long time to painstakingly design an image for every single blog post and every single documentation page. And we don't want the exact same image for every blog post because that wouldn't make the article stand out when it was shared to Twitter.

That's where `og-image.vercel.app` comes in. We can simply pass the title of our blog post to our generator service and it will generate the image for us on the fly!

It looks like the following:

```html
<head>
  <title>Hello World</title>
  <meta
    property="og:image"
    content="https://og-image.vercel.app/Hello%20World.png"
  />
</head>
```

Now try changing the text `Hello%20World` to the title of your choosing and watch the magic happen ✨

## Deploy your own

You'll want to fork this repository and deploy your own image generator.

1. Click the fork button at the top right of GitHub
2. Clone the repo to your local machine with `git clone URL_OF_FORKED_REPO_HERE`
3. Change directory with `cd og-image`
4. Make changes by swapping out images, changing colors, etc (see [contributing](https://github.com/vercel/og-image/blob/main/CONTRIBUTING.md) for more info)
5. Remove all configuration inside `vercel.json` besides `rewrites`
6. Run locally with `vercel dev` and visit [localhost:3000](http://localhost:3000) (if nothing happens, run `npm install -g vercel`)
7. Deploy to the cloud by running `vercel` and you'll get a unique URL
8. Connect [Vercel for GitHub](https://vercel.com/github) to automatically deploy each time you `git push` 🚀

## Authors

- Steven ([@styfle](https://twitter.com/styfle)) - [Vercel](https://vercel.com)
- Evil Rabbit ([@evilrabbit](https://twitter.com/evilrabbit_)) - [Vercel](https://vercel.com)
