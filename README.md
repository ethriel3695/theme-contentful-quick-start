---
slug: /gatsby-theme-contentful
label: Gatsby Theme Contentful
title: Gatsby Theme Contentful
description: A Gatsby Theme built using Contentful, Auth0, TailwindCSS, Gatsby, React, Graphql and Various other plugins
date: 2020-05-23
categories: ['react', 'node', 'gatsby', 'theme', 'contentful', 'tailwindCSS']
published: true
---

## Current Stack

**Auth0** - For authentication if the flag `isAuthApp` is set to true in `gatsby-config.js`

**TailwindCSS** - For small bundle size and easy to use css classes (Seriously the easiest!!!)

**MDX** - For page rendering based on markdown content (Files are added to `/content` directory)

**Contentful** - A headless CMS so content can be added by non-developers for pages, sections and widget rendering

## Current Limitations

1. Contentful is currently required and requires a page, section, item and image placeholder to render

**Workaround:** Add a Page and section named Placeholder Content with an Image and Item and the CMS will load correctly

2. At least one folder is required in `/content` and I use `/post/placeholder/placeholder.mdx`

### Example MDX config

```mdx
---
slug: /placeholder-content
label: Placeholder
title: Placeholder
description: Placeholder
date: 2020-05-21
categories: ['react', 'node']
published: false
---

## Placeholder
```

## Contentful Data schema

### Command to export Contentful Schema and Entries

```bash
contentful space export --save-file --management-Token=[ContentManagementAPIKey] --space-id=[SpaceID]
```

#### Page:

- Title: Short Text (250 characters)
- Description Long Text
- Page Type: Short text (250 characters) - Used to render specific page templates in the code
  - Currently supported page types: (HeroLanding)
- Slug: Short Text (250 Characters) - Page route for content
- Sections: References - One to many sections can be added to a page
- Author: Short Text
- Created Date: Date & Time
- categories: Short Text, List

#### Section:

- Title: Short Text (250 characters)
- Description: Rich Text
- Sub Header: Long Text
- Order: Integer

#### Item:

- Title: Short Text (250 characters)
- Sub Header: Short Text
- Link: Short Text (External Link)
- Slug: Short Text (Internal route)

#### Asset:

- Title: Short Text (250 characters)
- Asset Type: Short Text (Current Asset Types: Logo)
- File: Media

#### Call To Action:

- Title: Short Text (250 characters)
- Text: Long Text
- Button Text: Short Text
- Slug: Short Text
- External Link: Short Text

#### Multiple Call To Action:

- Title: Short Text (250 characters)
- Description: Rich Text
- Sub Header: Long Text
- Call To Action: References, many

#### Gallery:

- Title: Short Text (250 characters)
- Description: Rich Text
- Sub Header: Long Text
- Caption: Short Text
- Media: References, many

#### Hero:

- Title: Short Text (250 characters)
- Description: Rich Text
- Sub Header: Long Text
- File: Media

#### Media With Caption:

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

- Create a script to genarate the Contentful schema rather than having to create it manually
- Create a Live Demo to show functionality of different components and template setup
- Integrate Jest and Storybook into each component
- When a component is added, also add Jest and Storybook configurations automatically

## Quick start

<!-- TODO: Add docs on how to run the schema creation script using `yarn run setup` -->

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
1. <a
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

**NOTE:** Make sure to record the `spaceId`, `content management api access token` and `content delivery api access token`

Once you have the API keys, create a file in the root of your project named `.env`

and paste the following:

```
  # Do NOT commit this file to source control
  CONTENTFUL_SPACE_ID='${spaceId}'
  CONTENTFUL_MANAGEMENT_TOKEN='${managementToken}'
  CONTENTFUL_ACCESS_TOKEN='${accessToken}'
```

1.  **Create an Authenticated Site**

    In order to get an authentication enabled site up and going follow these steps:

    - Open a terminal of your choice **(Terminal on mac, Command Prompt, Powershell or Bash on Windows)**
    - Navigate to the directory where you store your repositories

    - Example:

      ```sh
      cd Users/[username]/source
      ```

    - Clone the authentication demo
      ```sh
       git clone https://github.com/ethriel3695/authentication-demo
      ```

2.  **Open the source code and start editing!**

    - Open the `authentication-demo` directory in your code editor of choice

## Additional configuration

In addition to the theme options, there are a handful of items you must modify via the `siteMetadata` object in your site's `gatsby-config.js`

The Social tags, if left as an empty string will not appear in the footer

### Authentication

Authentication now works out of the box if you provide the credentials in the `.env.development` and `.env.production` files
Also, in `gatsby-config.js` the `isAuthApp` key needs to be set to `true`
If you do not have an Auth0 account create one for free [Auth0](https://auth0.com/signup?&signUpData=%7B%22category%22%3A%22button%22%7D)

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
    title: `Site Title`,
    author: `Name of the Site Creator`,
    description: `Site Description`,
    greeting: `A more detailed description or greeting for the home page`,
    copyright: `Copyright message unique to site or company`,
    loginDesc:
      'If isAuthApp then this is the name of the button to login (ex: Login, Login / Signup)',
    isAuthApp: false, // default is true (If true, enables authentication)
    newsletterTitle: 'Text description of the newsletter button', // If empty no newsletter shows up in Header
    social: {
      facebook: 'altcampus',
      twitter: 'altcampus',
      github: 'ethriel3695',
      email: 'test@example.com',
    },
    externalLinks: [{ label: 'Google', link: 'https://www.google.com' }],
    hasNotifications: false, // Set to true if you want to enable notifications
  },
};
```

## Content directories

| Key           | Default value                | Description                                                                                                 |
| ------------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------- |
| `contentPath` | `/content/post`              | Directory for mdx content                                                                                   |
| `assetPath`   | `/content/assets`            | Location of assets                                                                                          |
| `logo`        | `/content/assets/logo`       | An image in the logo directory will replace the title in the header with a brand logo instead               |
| `newsletter`  | `/content/assets/newsletter` | A pdf in this directory will provide a static asset for a newsletter with the newsletter link in the header |
| `files`       | `/content/assets/files`      | A directory to store files for use across the website                                                       |
| `mdx`         | `true`                       | MDX renders the additional pages in the site currently and is used alongside contentful                     |

## Page/Post Creation MDX

- Create a `content` folder
- Create a `post` folder
- Create a folder such as `firstPost`
- Create an `mdx` file `firstPost.mdx`

## MDX file requirements

```mdx
---
slug: /sample
label: Navigation Text
title: Title of post
description: Description of post
date: Date post is written (Ex. 2020-02-07) (Not Required)
categories: ['react', 'node'] (Not currently rendered but in progress)
published: true
---
```

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
      section {
        title
        description {
          json
        }
        image {
          description
          fluid(maxWidth: 1904, quality: 100) {
            ...GatsbyContentfulFluid_noBase64
          }
        }
        slug
        order
        item {
          title
          subHeader
          link
          slug
        }
      }
    }
  }
}
```

## Environment variables

1. Create An `env.development` file to hold your environment variables
2. `env.production` to test when running `npm run build && npm run serve`

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
@tailwind base;

html body {
  @apply .bg-white .font-sans .antialiased;
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
  @apply text-2xl;

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
  @apply text-blue-600 underline;
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

@tailwind components;

.bgPrimary {
  @apply text-white bg-green-500;
}

.bgPrimary:hover {
  @apply bg-green-600;
}

.textPrimary {
  @apply text-green-500 !important;
}

.textPrimary:hover {
  @apply text-green-600 !important;
}

.borderPrimary {
  @apply border-green-500;

  @apply text-gray-900;
}

.borderPrimaryActive {
  @apply border-green-500 !important;

  @apply text-gray-900 !important;
}

.borderPrimary:hover {
  @apply border-green-500;
}

.swiper-pagination-bullet {
  @apply .bg-white;
}

.headerLogoSize {
  width: 6rem;
}

@tailwind utilities;

.container {
  @apply .max-w-screen-xl .mx-auto .px-4;
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
```
