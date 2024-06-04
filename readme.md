# Watson Docs
The Documentation site for Watson where all documentation around the entire project can be found.

---

The site is auto generated from markdown files using [DocFX](https://dotnet.github.io/docfx/). You can view the latest version of the docs site [here](https://xr-solutions.github.io/watson-docs/).

## Run the site locally
Since we use DocFx, the first step will be to make sure you have the tool installed. If you have the [dotnet cli](https://dotnet.microsoft.com/en-us/download) installed you can run the following command

```sh
dotnet tool install -g docfx
```

You can run the documentation website locally by running the following command in the root folder.

```sh
docfx docfx.json --serve 
```

If you then go to [http://localhost:8080](http://localhost:8080), you can view the website and monitor your changes.

## Making changes
Docs are written with [Markdown](https://daringfireball.net/projects/markdown/). DocFx supports [CommonMark](https://commonmark.org/) and quickly taking a look over the supported syntax is helpful. On the [DocFx markdown page](https://dotnet.github.io/docfx/docs/markdown.html), you can also quickly view the extra supported syntax such as [Alerts](https://dotnet.github.io/docfx/docs/markdown.html?tabs=linux%2Cdotnet).

Images should be placed within the images folder. If you are refering to an image within a markdown page, make sure to reference that image directly from the file you are in.

**Correct example**
```md
![Image alt tag](../images/image.png)
```

**Incorrect example**
```md
![Image alt tag](/images/image.png)
```

These examples both work locally, but when the page is built and hosted in github pages, the latter will not work. Also make sure to correctly include new pages in the `toc.yml` file when you create them. More information about the [table of content](https://dotnet.github.io/docfx/docs/table-of-contents.html) and docfx can be found on their own [docs site](https://dotnet.github.io/docfx/index.html).