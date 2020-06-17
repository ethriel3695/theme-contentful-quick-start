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

- Title: short Text (250 characters)
- Page Type: Short text (250 characters) - Used to render specific page templates in the code
  - Currently supported page types: (HeroLanding, Landing)
- Section: References - One to many sections can be added to a page
- Slug: Short Text (250 Characters) - Page path for content

#### Section:

- Title: Short Text (250 characters)
- Description: Rich Text
- Slug: Short Text (250 Characters) - Page path for content
- Order: Integer - The order that content appears on the page (Ascending)
- Item: References - One to many items can be added to a section
- Product: References - One to many products can be added to a section
- Image: Media - Used for a hero image
- Gallery:Media - Many files

#### Item: (Curently only renders as a button)

##### Future Functionality: Add various widget types to be rendered in the code by an `widgetType` or `itemType`

- Title: Short Text (250 characters)
- Sub Header: Short Text (250 characters)
- Link: Short Text (URL) (250 characters) - External links to other websites
- Slug: Short Text (Slug) - Path to one of the dynamically generated pages (MDX or Contentful)

### Product: (Render a list of products or services)

- Title: Short Text (250 characters)
- Description: Long Text (Markdown Rendering)
- Price: Short Text (250 characters)

## Future Additions

- Create a script to genarate the Contentful schema rather than having to create it manually
- Create a Live Demo to show functionality of different components and template setup
- Integrate Jest and Storybook into each component
- When a component is added, also add Jest and Storybook configurations automatically

## Quick start

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
