# Getting Started

## Installation

1. Add the following style tag to your `index.html` file:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@ky_wong/docsify-version-plugin@1.0.2/style.css">
```

2. Add the following script tag to your `index.html` file:

```html
<script src="https://cdn.jsdelivr.net/npm/@ky_wong/docsify-version-plugin@1.0.2/index.js"></script>
```

---

## Configuration

```html
<script>
    let versions = [
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

Set the default property to true for the version you want to display by default. 
The order of the array also defines the order in the dropdown.

Make sure the respective folder exists. Labels can be updated without the need to 
change the folder name.

### Detail Explanation

```txt
docsify-version-plugin-doc-example/
└── docs/
    ├── v1.0/
    │   ├── documentation/
    │   │   ├── getting-started.md
    │   │   └── theme.md
    │   ├── _navbar.md
    │   ├── _sidebar.md
    │   └── README.md
    ├── v2.0/
    │   ├── _navbar.md
    │   ├── _sidebar.md
    │   └── README.md
    ├── .nodekyll
    └── index.html
```

The `version[x].folder` value is based on the index.html. 

Actually this plugin will set the basePath value to the sessionStorage. The window.$docsify.basePath
will be set to the sessionStorage.getItem("basePath") value.

When the user select the version, the sessionStorage.getItem("basePath") will be updated and 
refresh the page. The window.$docsify.basePath will get the md file based the sessionStorage.getItem("basePath") value.


---

## Troubleshooting

### Search Plugin

Added `const versionFolder = sessionStorage.getItem("basePath");` before the `window.$docsify`. 
In the `search` configuration, create a separate name space for each version.

```html
<script>
    let versions = [
      { folder: 'v2.0', label: 'v2.x', default: true },
      { folder: 'v1.0', label: 'v1.x', default: false }
    ];
    let basePath = sessionStorage.getItem("basePath");
    if (basePath == null) {
      let defaultVersion = versions.find((v) => v.default).folder;
      sessionStorage.setItem("basePath", defaultVersion);
    } 
    const versionFolder = sessionStorage.getItem("basePath");
    
    window.$docsify = {
        // ... Other configuration options
        search: {
            maxAge: 86400000,
            placeholder: 'Type to search',
            noData: 'No results!',
            depth: 6,
            namespace: 'docs-' + versionFolder // Set a unique namespace for each version
        },
    }
</script>
```
