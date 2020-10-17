---
slug: /gatsby-theme-contentful
label: Gatsby Theme Contentful
title: Gatsby Theme Contentful
description: A Gatsby Theme built using Contentful, Auth0, TailwindCSS, Gatsby, React, Graphql and Various other plugins
date: 2020-05-23
categories: ['react', 'node', 'gatsby', 'theme', 'contentful', 'tailwindCSS']
published: true
---

## Bash Commands For the Terminal

`cd` navigates to a folder on your computer
`git clone` Allows you to copy a repository in Github
`cd [name of folder]` Takes you into folder
`code .` Opens visual studio code for the current folder directory

## Getting Started

**NOTE:** If you don't have a source folder then create one with `mkdir source`
It's beneficial to store all your repositories in a source folder

1. Open up a terminal, command line, etc.
2. Run the following commands:

```bash
cd /source #Press Enter

git clone https://github.com/ethriel3695/theme-contentful-quick-start.git #Enter

#Once the repository is done cloning, run

cd theme-contentful-quick-start #Enter
```

4. Open the repo in your favorite code editor

   - I use VS Code so I run

```bash
code . #Enter
```

5. When the repo is open either use the VS Code Terminal or regular terminal and run

```bash
yarn
```

**NOTE:** If yarn is not installed on your computer, follow the instructions
https://classic.yarnpkg.com/en/docs/install

## Contentful

1. Setup a <a href="https://www.contentful.com/sign-up/" target="_blank" rel="noopener noreferrer">Contentful</a> account
2. Choose the option to build a content rich App `For Developers`
3. Skip the static site setup and go to the home screen of your space
4. <a
   href="https://www.contentful.com/r/knowledgebase/creating-a-website-in-five-minutes/"
   target="\_blank"
   rel="noopener noreferrer"
   > Contentful
   > </a> guide for setup

Sections to look at:

- Create a new `data bucket`, or space, to store content
- Generate a Content Management API access token
- Generate a Content Delivery API access token

https://www.contentful.com/faq/basics/

https://www.contentful.com/developers/docs/references/authentication/

https://www.contentful.com/developers/docs/references/authentication/#the-content-management-api

5. Create an empty space in Contentful by following the Guide for Setup above
6. Generate a Content Management API access token

- Store key in notepad or other text editor

7. Generate a Content Delivery API access token

- Store key in notepad or other text editor

**NOTE:** Make sure to record the `spaceId`, `content management api access token` and `content delivery api access token`

Once you have the API keys, create a file in the root of your project named `.env`

and paste the following:

```
  # Do NOT commit this file to source control
  CONTENTFUL_SPACE_ID='${spaceId}'
  CONTENTFUL_MANAGEMENT_TOKEN='${managementToken}'
  CONTENTFUL_ACCESS_TOKEN='${accessToken}'
```

8. Replace the dollar sign, curly praces and placeholder text with your credentials you just
   copied from Contentful

9. Look at your `package.json` file and find the `setup` script
10. Go to the terminal and type `yarn run setup` and hit enter
11. Verify that the Content Models and Content have been created in Contentful
12. Create an `.env.development` file and paste the following:

```
GATSBY_CONTENTFUL_SPACEID=spaceId
GATSBY_CONTENTFUL_API=accessToken
GATSBY_GOOGLE_ANALYTICS_ID=placeholder
```

13. Create an `.env.production` file with the same credentials to test when
    running `yarn run test:build`

## Environment variables

1. Create An `env.development` file to hold your environment variables
2. `env.production` to test when running `npm run build && npm run serve`

3. In the terminal, type `yarn run develop` and enter

At this point, your web application runs and displays content

## Additional configuration

In addition to the theme options, there are a handful of items you must modify via the `siteMetadata` object in your site's `gatsby-config.js`

The Social tags, if left as an empty string will not appear in the footer

```js
// gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: 'gatsby-theme-contentful',
      options: {},
    },
  ],
  siteMetadata: {
    title: `Site Title`, // Changes the title of the website in the tab of the browser
    author: `Name of the Site Creator`, // metadata used by Google
    description: `Site Description`, // metadata used by Google
    greeting: `A more detailed description or greeting for the home page`,
    copyright: `Copyright message unique to site or company`,
    isAuthApp: false, // default is true (If true, enables authentication)
    newsletterTitle: 'Text description of the newsletter button', // If empty no newsletter shows up in Header
    social: {
      facebook: 'https://www.facebook.com/freecodecamp',
      twitter: 'https://twitter.com/freecodecamp',
      instagram: 'https://www.instagram.com/freecodecamp',
      github: 'https://www.github.com/ethriel3695',
      email: 'mailto:test@example.com',
    },
    externalLinks: [{ label: 'Google', link: 'https://www.google.com' }],
    hasNotifications: false, // Set to true if you want to enable notifications
  },
};
```

## Page Creation using MDX

In the `content/post` folder

- Create a folder named `firstPost`
- Create an `mdx` file `firstPost.mdx`

## MDX file requirements

```mdx
---
slug: /sample
label: Navigation Text
title: Title of post
description: Description of post
date: 2020-09-07
author: Article Creator Name
categories: ['react', 'node']
published: true
---
```

This will render the MDX as a page and add the `slug` to the navigation bar
This feature is useful if you want to test secondary pages quickly such as
adding a google calendar or maybe even an `About` page

### Reference for MDX Syntax

https://www.gatsbyjs.com/docs/mdx/markdown-syntax/

## Optional functionality for a Blog/Article setup

Run `yarn blog:setup` and you now have an ArticleSummary page and related articles

In order to have an article or blog on the site you need to add page content
in Contentful

1. Go to Contentful and click on the `Content` tab
2. Select `Page` as the Content Type
3. Fill out the following details:

- Title: Blog or Articles
- Description: Put in a brief summary
- Page Type: ArticleSummary
- Slug: /blog
- Sections: Select and existing section for now (The Placeholder Section)
- Author: Your Name
- Created Date: Select todays date
- categories: article (Press Enter), summary (Press Enter)

4. Publish the Page
5. Open your Terminal and press `ctrl + c` to stop the application
6. Type `yarn develop` to restart

You will now have the route for the Blog or Articles Summary show up
in the navigation bar

### Option 1: Create articles using MDX

If you want to create content quickly then you can create an article using MDX

```mdx
---
slug: /blog/sample
label: Navigation Text
title: Title of post
description: Description of post
date: 2020-09-07
author: Article Creator Name
categories: ['react', 'node', 'blog']
published: true
---
```

**NOTE:** The `/blog` is important in the `slug` because it will add this article
to the Article Summary page and make sure this article isn't added to the
navigation bar

**Also:** The `categories` array requires the `'blog'` option in order
for the article to show up

### Option 2: Create articles using Contentful

<!--TODO: Add the steps to create an article in Contentful -->

^^I've decided to bake this into a script and abstract it so the user can just have an example
I'm going to look into the docs on how to import just data into Contentful
and then write the Blog data and sample article into contentful through a running of a script
just like the setup process

## Content directories

| Key           | Default value                | Description                                                                                                 |
| ------------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------- |
| `contentPath` | `/content/post`              | Directory for mdx content                                                                                   |
| `assetPath`   | `/content/assets`            | Location of assets                                                                                          |
| `logo`        | `/content/assets/logo`       | An image in the logo directory will replace the title in the header with a brand logo instead               |
| `newsletter`  | `/content/assets/newsletter` | A pdf in this directory will provide a static asset for a newsletter with the newsletter link in the header |
| `files`       | `/content/assets/files`      | A directory to store files for use across the website                                                       |

## Create an optional Article section to display MDX files on the site

## Current Stack

**Auth0** - For authentication if the flag `isAuthApp` is set to true in `gatsby-config.js`

**TailwindCSS** - For small bundle size and easy to use css classes (Seriously the easiest!!!)

**MDX** - For page rendering based on markdown content (Files are added to the`content` directory)

**Contentful** - A headless CMS so content can be added by non-developers for pages, sections, images and more

## Current Limitations

1. Contentful is currently required for the quick start to work

**Workaround:** Follow the `Getting Started` guide below to create the content

2. At least one folder is required in `/content` and I use `/post/placeholder/placeholder.mdx`

### Example MDX config

```mdx
---
slug: /placeholder-content
label: Placeholder
title: Placeholder
description: Placeholder
date: 2020-05-21
author: placeholder
categories: ['react', 'node']
published: false
---

## Placeholder
```

## Contentful Data schema

### Page:

- Title: Short Text (250 characters)
- Description Long Text
- Page Type: Short text (250 characters) - Used to render specific page templates in the code
  - Currently supported page types: (HeroLanding)
- Slug: Short Text (250 Characters) - Page route for content
- Sections: References - One to many sections can be added to a page
- Author: Short Text
- Created Date: Date & Time
- categories: Short Text, List

### Section:

- Title: Short Text (250 characters)
- Description: Rich Text
- Sub Header: Long Text
- Order: Integer

### Item:

- Title: Short Text (250 characters)
- Sub Header: Short Text
- Link: Short Text (External Link)
- Slug: Short Text (Internal route)

### Asset:

- Title: Short Text (250 characters)
- Asset Type: Short Text (Current Asset Types: Logo)
- File: Media

### Call To Action:

- Title: Short Text (250 characters)
- Text: Long Text
- Button Text: Short Text
- Slug: Short Text
- External Link: Short Text

### Multiple Call To Action:

- Title: Short Text (250 characters)
- Description: Rich Text
- Sub Header: Long Text
- Call To Action: References, many

### Gallery:

- Title: Short Text (250 characters)
- Description: Rich Text
- Sub Header: Long Text
- Caption: Short Text
- Media: References, many

### Hero:

- Title: Short Text (250 characters)
- Description: Rich Text
- Sub Header: Long Text
- File: Media

### Media With Caption:

- Title: Short Text (250 characters)
- Caption: Short Text
- File: Media

### Product: (Render a list of products or services)

- Title: Short Text (250 characters)
- Description: Long Text (Markdown Rendering)
- Price: Short Text (250 characters)
- Files: Media, many files

### Products: (A list of the content model Product)

- Title: Short Text (250 characters)
- Description: Rich Text
- Sub Header: Long Text
- Product: References, many

## Future Additions

- Create a Live Demo to show functionality of different components and template setup
- Integrate Cypress and Storybook into each component
- When a component is added, also add Cypress and Storybook configurations automatically (Storybook Docs)

## Page/Post Creation with Contentful

You can now create a Page in contentful and the page/post will be generated in the application

### Gatsby PageQuery Example

```
query ThemeDefaultPageQuery($pageId: String) {
  allContentfulPage(filter: { id: { eq: $pageId } }) {
    nodes {
      id
      title
      slug
      pageType
      sections {
        ... on ContentfulSection {
          title
          description {
            json
          }
          subHeader {
            subHeader
          }
        }
        ... on ContentfulHero {
          title
          description {
            json
          }
          subHeader {
            subHeader
          }
          file {
            description
            fluid(maxWidth: 1904, quality: 100) {
              ...GatsbyContentfulFluid_noBase64
            }
          }
        }
        ... on ContentfulGallery {
          title
          description {
            json
          }
          subHeader {
            subHeader
          }
          caption
          media {
            title
            caption
            file {
              title
              description
              fluid(maxWidth: 400, quality: 100) {
                ...GatsbyContentfulFluid_noBase64
              }
            }
          }
        }
        ... on ContentfulProducts {
          title
          description {
            json
          }
          subHeader {
            subHeader
          }
          product {
            title
            description {
              description
            }
            price
            files {
              title
              description
              fluid(maxWidth: 400, quality: 100) {
                ...GatsbyContentfulFluid_noBase64
              }
            }
          }
        }
        ... on ContentfulMultipleCallToAction {
          title
          description {
            json
          }
          subHeader {
            subHeader
          }
          callToAction {
            title
            text {
              text
            }
            buttonText
            externalLink
            slug
          }
        }
      }
    }
  }
}
```

```js
// env.development
// Auth0 variables required only if isAuthApp set to true in gatsby-config.js
GATSBY_AUTH0_DOMAIN = domain.auth0.com; // Replace domain with your auth0 domain
GATSBY_AUTH0_CLIENT_ID = secret_client_id; // This ID can be found after creating an Application within Auth0 within the Application tab
GATSBY_AUTH0_CALLBACK_URL = `http://localhost:8000/callback`; //Remove the literal string character when replacing the callback url
GATSBY_AUTH0_REDIRECT_URL = `http://localhost:8000`; //Remove the literal string character when replacing the callback url

// Google Maps variables required only if you want to use the map
GATSBY_GOOGLE_MAPS_API_KEY = `Google maps api key`;
GATSBY_GOOGLE_LATITUDE = `Latitude position to render map marker`;
GATSBY_GOOGLE_LONGITUDE = `Longitude position to render map marker`;
GATSBY_GOOGLE_MAP_DESC = `Description of map marker`;

// Google calendar url if you want to embed the calendar
GATSBY_GOOGLE_CALENDAR_URL = `https://calendar.google.com/calendar/embed?src=[emailTextBefore@symbol]%40gmail.com&ctz=America%2FBoise`;

// Contentful credentials if you want to use contentful
GATSBY_CONTENTFUL_SPACEID = `space id from contentful`;
GATSBY_CONTENTFUL_API = `special token from contentful`;

// Google Analytics ID for tracking and user engagement
GATSBY_GOOGLE_ANALYTICS_ID = `Google Analytics ID`;
```

You will probably want to customize your site styles to personalize it. The files within `/src/gatsby-theme-contentful` _shadow_, or override, the files of the same name in the `gatsby-theme-contentful` package.
To learn more about this, check out the [guide to getting started with using the blog theme starter](http://gatsbyjs.org/docs/themes/using-a-gatsby-theme).

**`Example`**: `src/gatsby-theme-contentful/components/styles/style.css` and then edit the following classes accordingly:

Change the the primary background color from green to red:

```
.bgPrimary {
  @apply text-white bg-green-500;
}

to

.bgPrimary {
  @apply text-white bg-red-500;
}

```

### Override Default Theme Colors

```css
/** purgecss start ignore */
@tailwind base;
html body {
  @apply font-serif;
  @apply leading-loose;
  @apply antialiased;
}

h1 {
  @apply text-5xl;

  @apply font-bold;

  @apply my-2;
}

h2 {
  @apply text-4xl;

  @apply font-semibold;

  @apply my-2;
}

h3 {
  @apply text-3xl;

  @apply font-semibold;

  @apply my-2;
}

h4 {
  @apply text-2xl;

  @apply font-semibold;

  @apply my-2;
}

h5 {
  @apply text-xl;

  @apply font-semibold;

  @apply my-2;
}

h6 {
  @apply text-lg;

  @apply font-semibold;

  @apply my-2;
}

a {
  @apply text-purple-600;
  @apply no-underline;
}

p {
  @apply my-3;
}

article {
  @apply px-4;
}

ol {
  @apply list-decimal;
}

h4 + ul {
  @apply list-disc;
}

h5 + ul {
  @apply list-disc;
}

@tailwind components;

.bg-primary {
  @apply text-white bg-purple-700;
}

.bg-primary:hover {
  @apply bg-purple-800;
}

.text-primary {
  @apply text-purple-700 !important;
}

.text-primary:hover {
  @apply text-purple-800 !important;
}

.border-primary {
  @apply border-purple-700;

  @apply text-gray-900;
}

.border-primary:hover {
  @apply border-purple-700;
}

.border-primary-active {
  @apply border-purple-700 !important;

  @apply text-gray-900 !important;
}

.swiper-pagination-bullet {
  @apply .bg-white;
}

.header-logo-size {
  width: 5rem;
}

@tailwind utilities;

.container {
  @apply .max-w-screen-lg .mx-auto .px-4;
}

@screen md {
  .container {
    @apply .px-6;
  }

  .swiper-pagination-bullet {
    @apply .w-3 .h-3;
  }
}

@screen lg {
  .container {
    @apply .px-8;
  }
}
/* purgecss end ignore */
```
