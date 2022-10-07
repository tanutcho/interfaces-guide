# About NAS

For now, we have 3 NAS servers.

### NAS IP address

* [INTERFACES-I All team](https://n1-int.myds.me): n1-int.myds.me
* [INTERFACES-II Public-Private Dataset](https://n2-int.myds.me): n2-int.myds.me
* [INTERFACES-III Sleep team](https://n3-int.myds.me): TBA

{% code title="NAS-I: n1-int.myds.me" %}
```markup
volume1
├── /Nannapas                        # Private access
volume2
├── /home                            # Full access, 1 TB for each user
└── /Co-Working_Space
    └── <your-shared-sub-folder>     # Please make inherited permissions explicit!
    └── <your-shared-sub-folder>     # Please make inherited permissions explicit!
    └── <your-shared-sub-folder>     # Please make inherited permissions explicit!
```
{% endcode %}

<pre class="language-markup" data-title="NAS-II: n2-int.myds.me"><code class="lang-markup"># Read-only access for permitted group
volume1
<strong>├── /Confidential_datasets
</strong>├── /Public_datasets
├── /Processed_datasets
└── /Confidential_project</code></pre>

### Make inherited permissions on `Co-Working_Space`

1. Right-click on <mark style="color:green;">\<your-shared-sub-folder></mark>
2. Properties --> Permission --> Advanced options --> Make inherited permissions explicit
3. Click "Create" to give permission to a specific user or group
