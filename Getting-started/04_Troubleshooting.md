# Troubleshooting

## Configuring remote

First, check the output of

```
git remote -v
```

It should read something like

```
origin	git@github.com:ubco-biology/RepositoryName.git (fetch)
origin	git@github.com:ubco-biology/RepositoryName.git (push)
```

If it reads `https` or just `github.com` you can run the following

```
git remote set-url origin git@github.com:ubco-biology/RepositoryName.git
```

## Jekyll stripping YAML header from downloaded RMD files

GitHub Pages are powered by Jekyll behind the scenes. Jekyll is a static site generator that takes Markdown and HTML files and creates a complete static website. 

When a template RMD file has a YAML header embedded in it, Jekyll processes this file and strips the Markdown file of its header. One solution for this problem is to host the template RMD files on OSF rather than on GitHub. An OSF page was created for ubco-biology here: [https://osf.io/k58xv/](https://osf.io/k58xv/).

Simply highlight the folder for the course you are working on and click 'upload'. Then upload the template RMD file to OSF.


Then click on the uploaded file to open the landing page for the template RMD file. Copy the url for this landing page. 


To generate a direct download link from OSF, take the landing page for the document and precede the unique identifier with download. For example, if the url for the file is https://osf.io/76ma4, then download link is https://osf.io/download/76ma4


Insert this download link into the host RMD file where students will be downloading the template from. 
