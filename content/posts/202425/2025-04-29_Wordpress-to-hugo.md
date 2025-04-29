---
title: "Going from Wordpress to Hugo"
date: 2025-04-29
categories: 
  - "general"
  - "technology"
tags: 
  - "wordpress"
  - "hugo"
  - "static website"
  - "hosting"
  - "free"
---

I have been hosting [my website](https://www.naresh.se/) on the [hosting platform](https://www.one.com/) since the last 17+ years. It has been quite a journey and I learnt a lot of things about networking, hosting, website management, content creation, etc. It was ofcourse a [Wordpress (WP)](https://wordpress.com/) site. On the side, I had [phpbb (forums)](https://www.phpbb.com/), [GedView](https://www.gedview.org/), etc. The website helps me keep my thoughts in control and provides me a platform to voice my opinions, ideas, views, etc. on various topics. I can go back and read the posts/blogs to sketch and retrace information as needed. So the blog/posts help me organize and keep a record of my braindump. The blogs/posts are more or less static and do not change much. So having a heavy WP install and maintaing it is a resource intensive work. Regular updates, security patches, etc. are also a pain to maintain.

During these years, I have been offered a generous storage by the hosting platform (50GB), PHP support, email hosting (though I use only named aliases to redirect to my normal emails), etc. But otherwise, it was just a waste of money and resources. I have been using the platform for a long time and it has been a great experience. However, I have been thinking of moving to a more modern platform and I have been looking at [Hugo](https://gohugo.io/).

Hugo is a static website generator that is written in Go. It is a fast and efficient way to generate static websites. It is also a great way to host websites on GitHub Pages, GitLab Pages, etc. It is also a great way to host websites on [Netlify](https://www.netlify.com/), [Vercel](https://vercel.com/), [GitHub Pages](https://pages.github.com/), [GitLab Pages](https://pages.gitlab.com/), etc. One can read more about the differences between WP and Hugo [here](https://www.wpbeginner.com/beginners-guide/wordpress-vs-hugo/) and [here](https://mansoorbarri.medium.com/hugo-vs-wordpress-a-performance-and-seo-comparison-6f544e3bac4c#:~:text=Hugo%20is%20a%20static%20site%20generator%2C%20which%20means%20it%20doesn,less%20vulnerable%20to%20security%20threats.). I had already started the journey about 7 years ago and had hosted a backup on [Naresh netlify](https://naresh.netlify.app/). But in the back of my mind, I was still a bit hesitant to move entirely to Hugo because of some lack of functionality like searching posts, analytics, etc. Back then Hugo was still in its initial stages and did not have the same level of functionality as WP. But now, it has come a long way and I have been using it for a while now and it has been a great experience.

So I decided to move over entirely to Hugo. The migration was pretty simple. First step was to download the WP backup for all content. And then install the hugo distribution. The next step was to create a simple github repo for storing the website content. I decided on the zzo theme as it satisfies all my requirements. But the development for zzo has not kept pace with Hugo. So I forked it and hosted it on my [github](https://github.com/wolverine2k/hugo-theme-zzo). There is extensive documentation on how to configure the theme so please go through it. Then I used the [Wordpress export to Markdown](https://github.com/lonekorean/wordpress-export-to-markdown) to convert the WP backup into working markdown files to work with Hugo.

Once I checked that the Hugo website works as expected on my local machine, I hosted it on Netlify first. I had to update the DNS configs and AAA records to point to Netlify. But for some reason, I was not able to get the search to work. So I switched over to github pages instead. Similar procedure but Netlify migration was easier. Github took its own sweet time. So now my [main site](https://www.naresh.se/) is redirected from github pages. I have backup sites on [Netlify](https://naresh.netlify.app/), [Cloudflare](https://naresh-5j9.pages.dev/) and [Vercel](https://naresh-se.vercel.app/) just in case github does something weird or does not show up. I can run some scripts on my servers to probably redirect to the backup sites if needed (load sharing, etc.). But as of now, my website is quite nicely handling the traffic.

Between, I also plugged in Google Analytics on top of native analytics provided by Netlify, Cloudflare and Vercel. Gives me a very nice view of the traffic, reach, and a host of other parametric data. The best part is that it is easier to write blogs/posts using markdown and I don't need to worry about putting in extra plugins for functionality such as code-highlighting. My maintenance overhead is also close to zero (after doing the initial theme fiddling). And frankly I am quite happy with how this has turned out.

For the future, I am trying to get the GedView alternative to host side-by-side on github pages. I will post if I am able to get that done. Between, I have skimmed through how and where you need to update yhour AAA settings or get a certificate for https etc. Documentation for that is pretty clear on various hosting sites that I have listed here.

Go Hugo!
