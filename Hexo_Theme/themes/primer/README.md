> hexo/_config.yml

``` yaml
theme: primer
```

# Primer
## Personal Information

> theme/_config.yml

```yaml
profile:
	location: ChengDu #city
	github: yumemor #github id
	stackoverflow: #stackoverflow id
		title: 
		href: 
	organization: open #organization/company
```

## Github Repo Configure

``` yaml
github: 
	username: yumemor
  popular_repos: [hexo-theme-primer]
  # if show more repo [repo0, repo2, ...]
```

# Page
## Navigation

``` yaml
menus:
	- 
		name: Home
		link: /
	- 
		name: Category
		link: category/
		target: true # open a new label
```

## Open Source Projects

``` bash
hexo new page 'projects'
```

> projects/index.md

``` yaml
title: Open Source Projects
layout: projects
```

## Category

``` bash
hexo new page 'category'
```

> category/index.md

``` yaml
title: Category
layout: categories
```

## About

> about/index.md

```yaml
title: About
layout: about
```

## Links

> links/index.md

```yaml
title: Links
layout: about
```

## Message

``` bash
hexo new page 'message'
```

> message/index.md
``` yaml
title: 留言板
layout: page
share: false
toc: false
```

# Function

## Search

- install

``` bash
npm install hexo-generator-search --save
```

- configure

> hexo/_config.yml

``` yaml
#Search
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

> theme/_config.yml

```
search: google
```
! 默认为 `google` 搜索，本地搜索请修改为 `local`

## Comment
> theme/_config.yml

```yaml
comment:
	disqus_username: 
```

## Highlight

> hexo/_config.yml

``` yaml
highlight:
  	enable: true
	line_number: true
	auto_detect: false
	tab_replace:
```

# Article
## comment off

``` yaml
title: Hello World
comment: false
```

## Toc off (关闭目录)

``` yaml
title: Hello World
toc: false
```

## Share off

``` yaml
title: Hello World
share: false
```

## Rss
``` bash
npm install hexo-generator-feed --save
```
#Feed Atom
feed:
  type: atom
  path: atom.xml
  limit: 20