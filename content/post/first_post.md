+++
date = "2017-06-14T17:35:12+02:00"
categories = ["blog"]
tags = ["hugo","git hub pages","hosting"]
title = "First post"
+++

This is my first post. I used hugo to make this blog. I totally recommend it. Its easy and really quick to create a blog without the need to install anything extra(no plugins etc).  This was the easy part. 


I was struggling to deploy the hugo generated static website in github via /docs folder on master branch. It didn't work. Apparently having docs foler and hugo code on the same branch it does not work. The docs folder needs to be in a repo that it does not have name username.github.io.
Then I decided to separate the hugo code and generated output in two different repositories.  I googled around and I decided to follow the approach of hosting Personal/Organization Pages from [Hugo website](https://gohugo.io/tutorials/github-pages-blog/).


How to host hugo pages on github pages
-----------------

* 1. Created a repo with the name username.github.io for the hugo content. 
* 2. Created a repo with the name username.github.io-hugo for the generated static website.
* 3. Build by using :  hugo in the cmd.  Since the theme is defined in config.toml, there is no need to use the argument -t theme.
* 4. Delete the public folder that was created.
* 5. "git submodule add -b master https://github.com/username/username.github.io.git public". 
* 6. add a deploy.sh and copy the content from [Hugo website](https://gohugo.io/tutorials/github-pages-blog/). ***IMPORTANT***  change  hugo to ./hugo in order the script to work.
* 7. add and commit all the related files to hugo and push them to username.github.io-hugo
* 8. open cmd and use "icacls deploy.sh /reset" in order to remove any permission on this script. Or use [cmder] (http://cmder.net/) and execute the command : "chmod +x deploy.sh".
* 9. deploy.sh "Your optional commit message" Note: you need to have bash installed. I am using git bash which was installed together with git.


ENDING NOTES
-----------------
* I preferred to have two separate repo for separation of concern.One repo responsible for code and repo for hosting.
* I am using the hugo version [0.22.1] (https://github.com/gohugoio/hugo/releases/tag/v0.22.1).
* The source code of blog can be found on [GitHub] (https://github.com/lsimopoulos/lsimopoulos.github.io-hugo).


```
public class Application
{
	static void Main(string[] args)
	{
		Console.WriteLine("I posted my first post. yay !!");
	}
}
```