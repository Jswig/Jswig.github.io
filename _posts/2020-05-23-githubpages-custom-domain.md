---
title: "HTTPS on Github Pages with custom domains"
date: 2020-05-23
tags:
toc: false
---

Finding the correct way enabling HTTPS with a custom domain name on Github Pages took unexpectedly long, so I'll recap here the steps I followed in case they could be useful to someone else.
{: .text-justify}

The issue was that the "enforce HTTPS" button in the Github repo settings remained greyed out. The 
DNS provider is NameCheap, so YMMV with others. The official 
[github](https://help.github.com/en/github/working-with-github-pages/troubleshooting-custom-domains-and-github-pages#https-errors) 
[documentation](https://help.github.com/en/github/working-with-github-pages/securing-your-github-pages-site-with-https) 
on this was pretty unhelpful (it's possible that I am looking in the wrong place!)
Github correctly advises to configure your `CNAME` DNS with `www` host pointing to 
`<repo-name>.githun.io`. 
{: .text-justify}

However, the root of the issue was with `A` DNS records. Several of the top hits on Google incorrectly advise to create the following DNS `A` records:
{: .text-justify}

- `@` host, pointed to `192.30.252.153` 
- `@` host, pointed to `192.30.252.154`

Which did not work. It appears Github made changes that prevent accessing Pages sites over https 
on these IPs. This stackoverflow [answer](https://stackoverflow.com/a/9123911) by Ric Santos 
finally provided a solution: replace the above `A` records with the following:
{: .text-justify}

- `@` host, pointed to `185.199.108.153`
- `@` host, pointed to `185.199.109.153`
- `@` host, pointed to `185.199.110.153`
- `@` host, pointed to `185.199.111.153`

Which solved the issue after giving the the DNS changes time to propagate.
