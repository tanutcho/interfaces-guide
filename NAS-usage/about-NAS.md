# About NAS

For now, we have 3 NAS server.

### NAS IP address

* [INTERFACES-I All team](http://10.204.100.140:5000/): 10.204.100.140 - n1-int.myds.me
* [INTERFACES-II Public-Private Dataset](http://10.204.100.139:5000/): 10.204.100.139 - n2-int.myds.me
* [INTERFACES-III Sleep team](http://10.204.100.138:5000/): 10.204.100.138 - TBA

{% code title="NAS-I: n1-int.myds.me" %}
```markup
volume1
├── /Nannapas        #private access
│   └── <subfolder>
│   └── file1
volume2
├── /home            #Full access, 1 TB for each user
│   └── <subfolder>
│   └── file2
└── /Co-Working_Space
    └── <your-shared-sub-folder>         #Please make inherited permissions explicit
    └── <your-shared-sub-folder>         #Please make inherited permissions explicit
    └── <your-shared-sub-folder>         #Please make inherited permissions explicit
```
{% endcode %}

<pre class="language-markup" data-title="NAS-II: n2-int.myds.me"><code class="lang-markup"># Read-only access
volume1
<strong>├── /BCI-Public
</strong>├── /EXOBIC
├── /General-Private
│   └── /PSU
├── /Medical-Image-Private
├── /Sleep-Private
└── /Sleep-Public</code></pre>



### Create a Shared Folder

1. Go to NAS website (above links)
