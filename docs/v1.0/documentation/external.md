# External Markdown

You also can use this plugin to link git tags in your markdown files. 

**We can use the unprocessed versions of files stored in GitHub repositories.**

## Configuration

https://github.com/docsifyjs/docsify/  

`raw.githubusercontent.com/${user}/${repo}/${tag}/${path}`

```html
<script>
    let versions = [
        { folder: "https://raw.githubusercontent.com/docsifyjs/docsify/v4.13.1/docs/", label: "Docsify v4.13.1", default: false},
        { folder: "https://raw.githubusercontent.com/docsifyjs/docsify/v4.11.5/docs/", label: "Docsify v4.11.5", default: false},
        { folder: 'v2.0/', label: 'v2.x', default: false },
        { folder: 'v1.0/', label: 'v1.x', default: true }
    ];
    let basePath = sessionStorage.getItem("basePath");
    if (basePath == null) {
      let defaultVersion = versions.find((v) => v.default).folder;
      sessionStorage.setItem("basePath", defaultVersion);
    } 
    const versionFolder = sessionStorage.getItem("basePath");
    
    window.$docsify = {
        // ... Other configuration options
        basePath: sessionStorage.getItem("basePath"),
        versions: versions,
        versionSelectorLabel: 'Version',
    }
</script>
```