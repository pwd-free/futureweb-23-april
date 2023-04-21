---
author: Sean Emerson
title: "Astro 2.0 Pagination for Collections"
description: "How to use Astro 2.0 Pagination with collections of markdown files. This currently isnt clear with the Astro docs, but here is a simple explanation to get you started!"
date: 2022-02-16
draft: false
categories: [Astro]
tags: [astro, pagination, astro-bootstrap]
---

One of the biggest features of Astro 2.0 is content collections. They allow you to define type safe collections of markdown files, and access them with typescript type guarding. 

This post will go into how to paginate over a content collection. There are two options for creating a pagination page. You can use `[page].astro` for the filename and you will get `1.html`, `2.html` etc for your paginated pages. (This is documented on the Astro site)

A more conventional approach is to use `[...page].astro` which generates `index.html`, `2.html`, `3.html` which allows for a more natural page structure, as you will need an index page, and `index/1.html` is not very useful as an index page.

I will start with the code snippet that is available on the astro site 

```astro
---
// pages/blog/[...page].astro
// https://docs.astro.build/en/core-concepts/routing/#pagination
export async function getStaticPaths({ paginate }) {
  const astronautPages = [{
    astronaut: 'Neil Armstrong',
  }, {
    astronaut: 'Buzz Aldrin',
  }, {
    astronaut: 'Sally Ride',
  }, {
    astronaut: 'John Glenn',
  }];
  // Generate pages from our array of astronauts, with 2 to a page
  return paginate(astronautPages, { pageSize: 2 });
}
// All paginated data is passed on the "page" prop
const { page } = Astro.props;
---

<!--Display the current page number. Astro.params.page can also be used!-->
<h1>Page {page.currentPage}</h1>
<ul>
  <!--List the array of astronaut info-->
  {page.data.map(({ astronaut }) => <li>{astronaut}</li>)}
</ul>
```

Lets re-write that to get a collection (see my collections post for set up help) this example assumes your collection is called `blog`.

To do this you need to use `getCollection`

```astro
---
import { getCollection } from 'astro:content';
export async function getStaticPaths({ paginate }) {
  const pages = await getCollection('blog', ({ data }) => {
  return data.draft !== true;
});
  // Generate pages from our array of astronauts, with 2 to a page for testing
  return paginate(astronautPages, { pageSize: 2 });
}
// All paginated data is passed on the "page" prop
const { page } = Astro.props;
---
```

You then need to print the list of paginated pages, specific to the current page

```astro
---
...
const { page } = Astro.props;
---
  <h1>Blog Posts</h1>
  <ul>
    {page.data.map(({ data }) => <li><a href={`/blog/${slug}`}>{data.title}</a></li>)}
  </ul>
```

> Unfortunately you have to manually construct the url in the anchor tag. See example above.

You can then use the rest of the `page` properties to generate your pagination controls, and information. [See docs](https://docs.astro.build/en/reference/api-reference/#the-pagination-page-prop)


```astro
---
...
const { page } = Astro.props;
const { prev, next} = page.url;
---
  <h1>Blog Posts</h1>
  <ul>
    {page.data.map(({ data }) => <li>{data.title}</li>)}
  </ul>
  <p>Posts {page.start + 1} to {page.end + 1}</p>
  <p>{page.size} posts per page</p>
  <p>Page {page.currentPage} of {page.lastPage}</p>
  <p><a href={next}>Next Page</a></p>
  <p><a href={prev}>Previous Page</a></p>
```

If you would like to see an example of pagination controls, see my implementation in [Astro-Bootstrap](https://astro-bootstrap.github.io/components/pagination/)



