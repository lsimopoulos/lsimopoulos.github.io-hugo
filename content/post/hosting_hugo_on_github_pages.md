+++
date = "2017-06-14T17:35:12+02:00"
archives = ["2017/06"]
categories = ["hugo"]
tags = ["hugo","git hub pages","hosting"]
title = "Host Hugo on github pages"
author = "Leonidas Simopoulos"
+++

This is my first post. I used hugo to make this blog. I totally recommend it. It's really quick to create a blog without the need to install anything extra(no plugins etc). 


It took me some time to figure out how to host the blog on github pages. I was struggling to deploy the hugo generated static website in github via /docs folder on master branch. It didn't work. Apparently it does not work having docs folder and hugo code on the same branch. The docs folder needs to be in a repo that it does not have name username.github.io.
Then I decided to separate the hugo code and generated output in two different repositories.  I decided to follow the approach of hosting Personal/Organization Pages from [Hugo website](https://gohugo.io/tutorials/github-pages-blog/).


How to host hugo pages on github pages using windows os:
-----------------

* 1. Create a repo with the name username.github.io for the hugo content. 
* 2. Create a repo with the name username.github.io-hugo for the generated static website.
* 3. Build by using :  hugo in the cmd.  Since the theme is defined in config.toml, there is no need to use the argument -t theme.
* 4. Delete the public folder that was created.
* 5. "git submodule add -b master https://github.com/username/username.github.io.git public".  this line allows you to keep username.github.io repository in a subdirectory of username.github.io-hugo.
* 6. add a deploy.sh and copy the content from [Hugo website](https://gohugo.io/tutorials/github-pages-blog/). ***IMPORTANT***  change  hugo to ./hugo in order the script to work.
* 7. add and commit all the related files to hugo and push them to username.github.io-hugo
* 8. open cmd and use "icacls deploy.sh /reset" in order to remove any permission on this script. Or use [cmder] (http://cmder.net/) and execute the command : "chmod +x deploy.sh".
* 9. deploy.sh "Your optional commit message" Note: you need to have bash installed. I am using git bash which was installed together with git.


ENDING NOTES
-----------------
* I preferred to have two separate repo for separation of concern.One repo responsible for code and repo for hosting.
* I used the hugo version [0.23] (https://github.com/gohugoio/hugo/releases/tag/v0.23).
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