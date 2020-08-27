Symantec HTML naming

for example use the main tag for content in page

```
<main> </main>
```



use a head tag

```jsx
import Head from 'next/head';

<Head>
  <title>My page title</title>
</Head>
```



### Tags to always have

[documentation](https://moz.com/blog/the-ultimate-guide-to-seo-meta-tags)

***meta tag***

```html
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
```

Meta viewport

```html
<meta name=viewport content="width=device-width, initial-scale=1">
```





### Example 	

```jsx
import Head from 'next/head';

<Head>
  <title>My page title</title>
  <meta httpEquiv="Content-Type" content="text/html; charset=utf-8" />
	<meta name="description" content="a quick bit of detail about the site" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
</Head>
```

