---
id: serverconfig
title: Server Config
---

<pre style="display:none;">

Use https://jsfiddle.net/jbsu0pvk/1/ to get copied HTML source

overflow: auto hidden; margin-bottom: 16px;

</pre>


The server config is both a TypeScript interface, and a JSON file. The JSON file is loaded and normalized to match the ServerConfig interface definition and then type-checked to make sure all the data is valid. This helps me catch bugs during development and helps everyone make sure their settings.json file has the correct format.

<div style="display:none;">

```json
{
  // comments are allowed in the config JSON.
  // these are the important ones
  "$schema": "./tiddlyserver-2-2.schema.json",
  "tree": {}, // or "tiddlyserver.xml",
  "authAccounts": {},
  "bindInfo": {},
  "putsaver": {},
  // the rest of these options are not as important
  "directoryIndex": {},
  "datafolder": {},
  "authCookieAge": 86400,
  "maxTransferRequests": 20,
  "debugLevel": 0,
  "_datafolderserver": "",
  "_datafolderclient": ""
}
```

</div>

<meta charset='utf-8'><div style="color: #000000;background-color: #ffffff;font-family: Menlo, Monaco, 'Courier New', monospace;font-weight: normal;font-size: 12px;line-height: 18px;white-space: pre; overflow: auto hidden; margin-bottom: 16px;"><div><span style="color: #000000;">{</span></div><div><span style="color: #000000;">  </span><span style="color: #008000;">// comments are allowed in the config JSON.</span></div><div><span style="color: #000000;">  </span><span style="color: #008000;">// these are the important ones</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"$schema"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"./tiddlyserver-2-2.schema.json"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"tree"</span><span style="color: #000000;">: {}, </span><span style="color: #008000;">// or "tiddlyserver.xml",</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"authAccounts"</span><span style="color: #000000;">: {},</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"bindInfo"</span><span style="color: #000000;">: {},</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"putsaver"</span><span style="color: #000000;">: {},</span></div><div><span style="color: #000000;">  </span><span style="color: #008000;">// the rest of these options are not as important</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"directoryIndex"</span><span style="color: #000000;">: {},</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"datafolder"</span><span style="color: #000000;">: {},</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"authCookieAge"</span><span style="color: #000000;">: </span><span style="color: #098658;">86400</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"maxTransferRequests"</span><span style="color: #000000;">: </span><span style="color: #098658;">20</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"debugLevel"</span><span style="color: #000000;">: </span><span style="color: #098658;">0</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"_datafolderserver"</span><span style="color: #000000;">: </span><span style="color: #a31515;">""</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"_datafolderclient"</span><span style="color: #000000;">: </span><span style="color: #a31515;">""</span></div><div><span style="color: #000000;">}</span></div></div>

## Section `tree` (required)

The tree property may be a string or an object. If it is a string end in `json`, it is loaded and parsed as JSON. If it is a string ending in `xml` it is loaded as an XML document and converted to JSON. 

The tree property has many expressions, but compiles to one final structure. In it's simple form, it is expressed as string values specifying folders and files to be served organized into a tree structure using objects.

<div style="display:none;">

```json
{
  "tree": {
    "myfolder": "../personal",
    "work": "../work",
    "user": "~/Desktop/random",
    "projects_group": {
      "tiddlyserver": "~/Desktop/Github/TiddlyServer",
      "material-theme": "~/Dropbox/Material Theme"
    }
  }
}
```

</div>

<div style="color: #000000;background-color: #ffffff;font-family: Menlo, Monaco, 'Courier New', monospace;font-weight: normal;font-size: 12px;line-height: 18px;white-space: pre; overflow: auto hidden; margin-bottom: 16px;"><div><span style="color: #000000;">{</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"tree"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"myfolder"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"../personal"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"work"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"../work"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"user"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"~/Desktop/random"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"projects_group"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"tiddlyserver"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"~/Desktop/Github/TiddlyServer"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"material-theme"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"~/Dropbox/Material Theme"</span></div><div><span style="color: #000000;">    }</span></div><div><span style="color: #000000;">  }</span></div><div><span style="color: #000000;">}</span></div></div>

In it's advanced form it is a separate XML document with element names, attributes, and children. A folder element only has option elements, but a group element may contain other group and folder elements as well as the same option elements. Here is that same tree, with an auth element added to one folder

<div style="display:none;">

```xml
<tree>
  <folder key="myfolder" path="../personal">
    <!-- this folder can only be accessed by users in the admin group -->
    <auth authError="403">
      <authList>admin</authList>
    </auth>
  </folder>
  <!-- the key is optional for folders (the folder name is used instead) -->
  <folder path="../work"/>
  <folder key="user" path='~/Desktop/random'/>
  <!-- but required for groups -->
  <group key="projects_group">
    <folder path="~/Desktop/GitHub/TiddlyServer"/>
    <folder key="material-theme" path="~/Dropbox/Material Theme">
  </group>
</group>
```

</div>

<div style="color: #000000;background-color: #ffffff;font-family: Menlo, Monaco, 'Courier New', monospace;font-weight: normal;font-size: 12px;line-height: 18px;white-space: pre; overflow: auto hidden; margin-bottom: 16px;"><div><span style="color: #800000;">&lt;tree&gt;</span></div><div><span style="color: #000000;">  </span><span style="color: #800000;">&lt;folder</span><span style="color: #000000;"> </span><span style="color: #ff0000;">key</span><span style="color: #000000;">=</span><span style="color: #0000ff;">"myfolder"</span><span style="color: #000000;"> </span><span style="color: #ff0000;">path</span><span style="color: #000000;">=</span><span style="color: #0000ff;">"../personal"</span><span style="color: #800000;">&gt;</span></div><div><span style="color: #000000;">    </span><span style="color: #008000;">&lt;!-- this folder can only be accessed by users in the admin group --&gt;</span></div><div><span style="color: #000000;">    </span><span style="color: #800000;">&lt;auth</span><span style="color: #000000;"> </span><span style="color: #ff0000;">authError</span><span style="color: #000000;">=</span><span style="color: #0000ff;">"403"</span><span style="color: #800000;">&gt;</span></div><div><span style="color: #000000;">      </span><span style="color: #800000;">&lt;authList&gt;</span><span style="color: #000000;">admin</span><span style="color: #800000;">&lt;/authList&gt;</span></div><div><span style="color: #000000;">    </span><span style="color: #800000;">&lt;/auth&gt;</span></div><div><span style="color: #000000;">  </span><span style="color: #800000;">&lt;/folder&gt;</span></div><div><span style="color: #000000;">  </span><span style="color: #008000;">&lt;!-- the key is optional for folders (the folder name is used instead) --&gt;</span></div><div><span style="color: #000000;">  </span><span style="color: #800000;">&lt;folder</span><span style="color: #000000;"> </span><span style="color: #ff0000;">path</span><span style="color: #000000;">=</span><span style="color: #0000ff;">"../work"</span><span style="color: #800000;">/&gt;</span></div><div><span style="color: #000000;">  </span><span style="color: #800000;">&lt;folder</span><span style="color: #000000;"> </span><span style="color: #ff0000;">key</span><span style="color: #000000;">=</span><span style="color: #0000ff;">"user"</span><span style="color: #000000;"> </span><span style="color: #ff0000;">path</span><span style="color: #000000;">=</span><span style="color: #0000ff;">'~/Desktop/random'</span><span style="color: #800000;">/&gt;</span></div><div><span style="color: #000000;">  </span><span style="color: #008000;">&lt;!-- but required for groups --&gt;</span></div><div><span style="color: #000000;">  </span><span style="color: #800000;">&lt;group</span><span style="color: #000000;"> </span><span style="color: #ff0000;">key</span><span style="color: #000000;">=</span><span style="color: #0000ff;">"projects_group"</span><span style="color: #800000;">&gt;</span></div><div><span style="color: #000000;">    </span><span style="color: #800000;">&lt;folder</span><span style="color: #000000;"> </span><span style="color: #ff0000;">path</span><span style="color: #000000;">=</span><span style="color: #0000ff;">"~/Desktop/GitHub/TiddlyServer"</span><span style="color: #800000;">/&gt;</span></div><div><span style="color: #000000;">    </span><span style="color: #800000;">&lt;folder</span><span style="color: #000000;"> </span><span style="color: #ff0000;">key</span><span style="color: #000000;">=</span><span style="color: #0000ff;">"material-theme"</span><span style="color: #000000;"> </span><span style="color: #ff0000;">path</span><span style="color: #000000;">=</span><span style="color: #0000ff;">"~/Dropbox/Material Theme"</span><span style="color: #800000;">&gt;</span></div><div><span style="color: #000000;">  </span><span style="color: #800000;">&lt;/group&gt;</span></div><div><span style="color: #800000;">&lt;/group&gt;</span></div></div>

The end result is exactly the same (except for the auth element). The XML document and the simple JSON are both converted to a JSON document in the advanced format. This is the internal structure that TiddlyServer uses.

In the config file the simple and advanced formats may be mixed. Any object which doesn't contain the `$element` property is converted into a Group element. Any string is converted to a Folder element.

In the advanced format, the `$element` property corrosponds to the XML tag name. The `$children` property corrosponds to the XML children. All other properties corrospond to XML attributes. Unlike JSON, all attribute values must be quoted (e.g. `<folder noDataFolder=true>` should be `...="true"`). The `$options` property is allowed in JSON to separate the children and option elements. Now, let's put that all together. Here is the same tree again with some more combinations. Read the comments.

<div style="display:none;">

```json
{
  "tree": {
    "myfolder": {
      //the $element property triggers the advanced syntax
      "$element": "folder",
      "path": "../personal",
      //the $options element is provided for clarity
      "$options": [
        {
          "$element": "auth",
          "authList": ["admin"],
          "authError": 403
        }
      ]
      //a folder has no other children
    },
    "work": "../work",
    "user": "~/Desktop/random",
    "projects_group":{
      "$element": "group",
      //the $children element can mix these formats as well, here it's just another tree
      "$children":  {
        "tiddlyserver": "~/Desktop/Github/TiddlyServer",
        "material-theme": "~/Dropbox/Material Theme",
        "more_mixed_levels": {
          "$element": "group",
          "$children": [
            "nothing to see here, I'm a valid folder, even if I don't exist"
          ]
        }
      }
    },
    //folders can be specified in an array
    "another_group": [
      "~/Desktop/hello world",
      "~/Downloads/more folders"
    ],
    //groups can be used to organize
    "my_pictures": {
      "home_photos": "~/Pictures",
      "work_photos": "~/Dropbox/jobsites"
    }
  }
}
```

</div>

<div style="color: #000000;background-color: #ffffff;font-family: Menlo, Monaco, 'Courier New', monospace;font-weight: normal;font-size: 12px;line-height: 18px;white-space: pre; overflow: auto hidden; margin-bottom: 16px;"><div><span style="color: #000000;">{</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"tree"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"myfolder"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">      </span><span style="color: #008000;">//the $element property triggers the advanced syntax</span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"$element"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"folder"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"path"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"../personal"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">      </span><span style="color: #008000;">//the $options element is provided for clarity</span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"$options"</span><span style="color: #000000;">: [</span></div><div><span style="color: #000000;">        {</span></div><div><span style="color: #000000;">          </span><span style="color: #0451a5;">"$element"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"auth"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">          </span><span style="color: #0451a5;">"authList"</span><span style="color: #000000;">: [</span><span style="color: #a31515;">"admin"</span><span style="color: #000000;">],</span></div><div><span style="color: #000000;">          </span><span style="color: #0451a5;">"authError"</span><span style="color: #000000;">: </span><span style="color: #098658;">403</span></div><div><span style="color: #000000;">        }</span></div><div><span style="color: #000000;">      ]</span></div><div><span style="color: #000000;">      </span><span style="color: #008000;">//a folder has no other children</span></div><div><span style="color: #000000;">    },</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"work"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"../work"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"user"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"~/Desktop/random"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"projects_group"</span><span style="color: #000000;">:{</span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"$element"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"group"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">      </span><span style="color: #008000;">//the $children element can mix these formats as well, here it's just another tree</span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"$children"</span><span style="color: #000000;">:  {</span></div><div><span style="color: #000000;">        </span><span style="color: #0451a5;">"tiddlyserver"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"~/Desktop/Github/TiddlyServer"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">        </span><span style="color: #0451a5;">"material-theme"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"~/Dropbox/Material Theme"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">        </span><span style="color: #0451a5;">"more_mixed_levels"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">          </span><span style="color: #0451a5;">"$element"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"group"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">          </span><span style="color: #0451a5;">"$children"</span><span style="color: #000000;">: [</span></div><div><span style="color: #000000;">            </span><span style="color: #a31515;">"nothing to see here, I'm a valid folder, even if I don't exist"</span></div><div><span style="color: #000000;">          ]</span></div><div><span style="color: #000000;">        }</span></div><div><span style="color: #000000;">      }</span></div><div><span style="color: #000000;">    },</span></div><div><span style="color: #000000;">    </span><span style="color: #008000;">//folders can be specified in an array</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"another_group"</span><span style="color: #000000;">: [</span></div><div><span style="color: #000000;">      </span><span style="color: #a31515;">"~/Desktop/hello world"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">      </span><span style="color: #a31515;">"~/Downloads/more folders"</span></div><div><span style="color: #000000;">    ],</span></div><div><span style="color: #000000;">    </span><span style="color: #008000;">//groups can be used to organize</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"my_pictures"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"home_photos"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"~/Pictures"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"work_photos"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"~/Dropbox/jobsites"</span></div><div><span style="color: #000000;">    }</span></div><div><span style="color: #000000;">  }</span></div><div><span style="color: #000000;">}</span></div></div>



It can look confusing with some simple and some advanced, but once you get used to it, it's not bad. If you like XML, feel free. 

> Advanced Feature: Internally, the tree property has an array of Host instances at the top level, but TiddlyServer simply uses the first Host in the array, unless the [preflighter](Preflighter.md) specifies a different host index. There are no plans to expand this feature, it is simply there for advanced use-cases.

### Group element type

- `$element`: `group`,
- `indexPath`: string,
- `key`: string - not used if specified in a hashmap instead of an array
- `$children`: An array or hashmap of Group and Folder elements
- `$options`: An array of Option elements

In XML: Group, Folder, and Option elements are all be mixed together as child elements.

### Folder element type

- `$element`: `folder`,
- `path`: string,
- `key`: string
  - not used if specified in a hashmap instead of an array
- `noDataFolder`: boolean
  - don't recognize data folders under this path (useful for your Downloads folder)
- `noTrailingSlash`: boolean
  - Mount data folders inside this folder without a trailing slash, so that relative links start at the folder instead of the data folder. This is usually not preferred, because the folder can be referred to with two dots `../` but it can be helpful when converting single file wikis to data folders and there are a lot of interwiki links involved.
- `$options`: An array of Option elements

### Option element types

The option elements can be specified on a group or folder element and apply to all children of that element, unless overriden by an option element for an element below it. Each option element overrides the properties of the element above it, unless the property is undefined. Here is a simple xml example of this.

#### Auth option

- `$element`: `auth`
- `authList`: Array of strings that are the keys from the authAccounts object. These auth accounts are allowed to access this resource. To allow anyone to access a child folder set this to null on that child folder.
- `authError`: Either `403` or `404`, as desired. The default is 403.

#### Putsaver option

- `$element`: `backups`
- `enabled`: Whether to allow the put saver to function on this path. The default is true.
- `backupFolder`: The folder path to put backups in. An empty string disables backups for this element.
- `etag`: Whether to use the etag field -- if not specified then it will check it if presented. This does not affect the backup etagAge option, as the saving mechanism will still send etags back to the browser, regardless of this option.
- `etagAge`: Don't save a backup unless the previous backup is older than this.
- `gzipBackups`: Whether to gzip compress the backup file to save space (highly recommended).

#### Index option

- `$element`: `index`
- `defaultType`: The type of directory index to return if no index file is found. `"html"`, `"json"`, `403`, `404`
- `indexFile`: Array of index file names to check for.
- `indexExts`: Array of index file extensions to use when checking for index.

`indexFile` and `indexExts` must both apply to the request in order for the index file to be used, but they don't need to be specified on the same element. For instance, one may be specified on a group, and the other may be specified on the folder underneath it.

## Section `authAccounts`

Auth accounts is a hashmap. The key is the account ID and the value is an object with two properties.

- `permissions` - The same permissions object specified in `bindInfo.localAddressPermissions`.
- `clientKeys` - A hashmap of { [`username`]: { `publicKey`: , `cookieSalt` } }

<div style="display:none">

```json
{
  "authAccounts": {
    "designteam": {
      "clientKeys": {
        "arlen": { "publicKey": "", "cookieSalt": "" }
      }, 
      "permissions": {
        // refer to the permissions object
      }
    }
  }
}
```

</div>

<div style="color: #000000;background-color: #ffffff;font-family: Menlo, Monaco, 'Courier New', monospace;font-weight: normal;font-size: 12px;line-height: 18px;white-space: pre; overflow: auto hidden; margin-bottom: 16px;"><div><span style="color: #000000;">{</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"authAccounts"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"designteam"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"clientKeys"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">        </span><span style="color: #0451a5;">"arlen"</span><span style="color: #000000;">: { </span><span style="color: #0451a5;">"publicKey"</span><span style="color: #000000;">: </span><span style="color: #a31515;">""</span><span style="color: #000000;">, </span><span style="color: #0451a5;">"cookieSalt"</span><span style="color: #000000;">: </span><span style="color: #a31515;">""</span><span style="color: #000000;"> }</span></div><div><span style="color: #000000;">      }, </span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"permissions"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">        </span><span style="color: #008000;">// refer to the permissions object</span></div><div><span style="color: #000000;">      }</span></div><div><span style="color: #000000;">    }</span></div><div><span style="color: #000000;">  }</span></div><div><span style="color: #000000;">}</span></div></div>

The page at `/admin/authenticate/login.html` will generate the public key based on the username and password and use it to log into the server, but the server does not care what method is used to generate the public key. We could just as easily implement a password-protected private key instead of hashing the username and password.

If the login fails, and the request has registerNotice set (by default this is only localhost requests), TiddlyServer will print a message to the terminal listing the username and generated publicKey, which you can copy and paste into your settings.json file as the `"base64string"` in the example above.

The username is passed to TiddlyWiki data folder instances for each request.

The public key is an ed25519 public key generated by the libsodium library function `crypto_sign_seed_keypair`.

The cookie salt is appended to the login cookie before it is sent in the Set-Cookie header. TiddlyServer checks the salt on every cookie to make sure it is correct for that user, so the user can be logged out of all devices if desired simply by changing the cookie salt. It must be a non-zero-length string, but otherwise it's value is completely meaningless.

If the cookie salt is changed to a string which was already used before for that user, any cookies set while that salt was active will become active again. Therefore it is recommended to use the current timestamp for the cookie salt whenever it is necessary to change it. All users may use the same cookie salt as long as they have never used it before.

Running the command `node -e "console.log(Date.now())"` will print the current timestamp.

## Section `bindInfo`

The bind info relates to the NodeJS server instances that TiddlyServer uses to recieve requests.

<div style="display:none">

```json
{
  "bindInfo": {
    "port": 8080,
    "bindAddress": ["127.0.0.1"],
    "bindWildcard": false,
    "enableIPv6": false,
    "filterBindAddress": false,
    "https": "./https.js",
    "localAddressPermissions": {
      "*": {
        // refer to the permissions object
      }
    },
    "_bindLocalhost": false
  }
}
```

</div>

<div style="color: #000000;background-color: #ffffff;font-family: Menlo, Monaco, 'Courier New', monospace;font-weight: normal;font-size: 12px;line-height: 18px;white-space: pre; overflow: auto hidden; margin-bottom: 16px;"><div><span style="color: #000000;">{</span></div><div><span style="color: #000000;">  </span><span style="color: #0451a5;">"bindInfo"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"port"</span><span style="color: #000000;">: </span><span style="color: #098658;">8080</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"bindAddress"</span><span style="color: #000000;">: [</span><span style="color: #a31515;">"127.0.0.1"</span><span style="color: #000000;">],</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"bindWildcard"</span><span style="color: #000000;">: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"enableIPv6"</span><span style="color: #000000;">: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"filterBindAddress"</span><span style="color: #000000;">: </span><span style="color: #0000ff;">false</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"https"</span><span style="color: #000000;">: </span><span style="color: #a31515;">"./https.js"</span><span style="color: #000000;">,</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"localAddressPermissions"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">      </span><span style="color: #0451a5;">"*"</span><span style="color: #000000;">: {</span></div><div><span style="color: #000000;">        </span><span style="color: #008000;">// refer to the permissions object</span></div><div><span style="color: #000000;">      }</span></div><div><span style="color: #000000;">    },</span></div><div><span style="color: #000000;">    </span><span style="color: #0451a5;">"_bindLocalhost"</span><span style="color: #000000;">: </span><span style="color: #0000ff;">false</span></div><div><span style="color: #000000;">  }</span></div><div><span style="color: #000000;">}</span></div></div>

### port: number;

port to listen on, default is 8080 for http and 8443 for https

### bindAddress: string[];

An array of IP addresses to accept requests on. Can be any IP address
assigned to the machine. Default is "127.0.0.1".

If `bindWildcard` is true, each connection is checked individually to make sure it is connected to one of the specified IP addresses. If `bindWildcard` is false, the server listens on the specified IP addresses and accepts all connections from the operating system. If an IP address cannot be bound, the server skips it unless `--bindAddressRequired` is specified.

If `filterBindAddress` is true, IPv4 addresses may include a subnet mask,
(e.g. `/24`) which matches any interface IP address in that range. Prefix with a minus sign (-)
to block requests incoming to that IP address or range.

### filterBindAddress: boolean;

Allow `bindAddress` items to include a subnet mask which will make it match a range of IP addresses instead of only one IP address.

### bindWildcard: boolean;

Bind to the wildcard addresses `0.0.0.0` and `::` (if enabled) in that order.
The default is `true`. In many cases this is preferred, however
Android does not support this for some reason. On Android, set this to
`false` and set host to `["0.0.0.0/0"]` to bind to all IPv4 addresses.

### enableIPv6: boolean;

Bind to the IPv6 wildcard as well if `bindWilcard` is true and allow requests
incoming to IPv6 addresses if not explicitly denied.

### localAddressPermissions: Hashmap

Permissions based on local address: "localhost", "\*" (all others), "192.168.0.0/16", etc.
This checks the server IP address each client actually connects to (socket.localAddress),
not the bind address of the server instance that accepted the request, so it works with bindWildcard. The localhost key will be used for all localhost requests regardless of the actual IP address.

- `datafolder`: Whether clients may access data folders, which gives them full access to the system as the user that owns the server process because data folders can be easily modified to execute code on the server. This returns a 403 Access Denied if a data folder is detected. It does not serve the files inside the data folder as a regular folder. For that you need to use the noDataFolder attribute on the folder in the tree.
- `loginlink`: Whether to include a link to the login page when returning auth errors
- `mkdir`: Whether clients may create new directories and datafolders inside existing directories served by TiddlyWiki
- `putsaver`: Whether clients may use the put saver, allowing any file served within the tree (not assets) to be overwritten, not just TiddlyWiki files. The put saver cannot save to data folders regardless of this setting.
- `registerNotice`: Whether login attempts for a public/private key pair which has not been registered will be logged at debug level 2 with the full public key which can be copied into an authAccounts entry. Turn this off if you get spammed with login attempts.
- `transfer`: Allows clients to use a custom TiddlyServer feature which relays a connection between two clients.
- `upload`: Whether clients may upload files to directories (not data folders).
- `websockets`: Whether clients may open websocket connections.
- `writeErrors`: Whether to write status 500 errors to the browser, possibly including stack traces.

Here is a good default for the standard use case.

```json
{
  "datafolder": true,
  "loginlink": true,
  "mkdir": false,
  "putsaver": true,
  "registerNotice": true,
  "transfer": false,
  "upload": false,
  "websockets": true,
  "writeErrors": false,
}
```

### \_bindLocalhost: boolean;

Always bind a separate server instance to 127.0.0.1 regardless of any other settings

## Section `putsaver`

Setting this property to false disables the putsaver completely in case this feature is not desired. The properties are the same as the putsaver option element in the tree. This can be considered the top-level `putsaver` option element and setting .

<div style="color: rgb(0, 0, 0); font-family: Menlo, Monaco, &quot;Courier New&quot;, monospace; font-size: 12px; line-height: 18px; white-space: pre; overflow: auto hidden; margin-bottom: 16px;"><div style="line-height: 18px;"><div style="line-height: 18px;"><div style="line-height: 18px;"><div>&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"putsaver"</span>:&nbsp;{</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"backupFolder"</span>:&nbsp;<span style="color: rgb(163, 21, 21);">"../backups"</span>,</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"etag"</span>:&nbsp;<span style="color: rgb(163, 21, 21);">"optional"</span>,</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"etagAge"</span>:&nbsp;<span style="color: rgb(9, 136, 90);">3</span>,</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"gzipBackups"</span>:&nbsp;<span style="color: rgb(0, 0, 255);">true</span></div><div>&nbsp;&nbsp;},</div></div></div></div></div>

### enabled: boolean

Set this to false to disable the putsaver.

### backupFolder: string

Backup directory to use for all single-file wikis. An empty string will disable backups.

### gzipBackups: boolean

Whether to gzip compress the backup file. The `.gz` extension will be added. Default is true. Files can be uncompressed using `tiddlyserver --gunzip backup.gz backup.html`.

### etag: string

Whether to use etag checking.

- `"disabled"` - Ignore the Etag.
- `"optional"` - Use it if sent by the client. This is the default.
- `"required"` - Require an Etag to be present.

### etagAge: number

This sets the number of seconds after which a copy is considered stale. This feature is hard to explain, but it was implemented because users often found that the modification time on disc would change by about two or three seconds after the file was saved, causing subsequent saves to be rejected.

Since a single user is not going to make changes to the same copy on two computers and save them both within 5-10 seconds of each other, 8 seconds is probably a safe number to use. The default, however, is 3.

If multiple users are editing the same file, you should probably be using Git or Dropbox to sync your changes instead of TiddlyServer. Or use a datafolder instead.

If the file size has changed, it is always considered stale, regardless of this setting.

## Section `directoryIndex`

A group of settings which apply to the directory index.

The example here demonstrates the difference between `icons` and `mimetypes`. `icons` needs to have _all_ extensions specified, and `mimetypes` only needs _additional_ extensions specified.

<div style="color: rgb(0, 0, 0); font-family: Menlo, Monaco, &quot;Courier New&quot;, monospace; font-size: 12px; line-height: 18px; white-space: pre; overflow: auto;"><div style="line-height: 18px;"><div style="line-height: 18px;"><div style="line-height: 18px;"><div style="line-height: 18px;"><div>&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"directoryIndex"</span>:&nbsp;{</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"defaultType"</span>:&nbsp;<span style="color: rgb(163, 21, 21);">"html"</span>,</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"icons"</span>:&nbsp;{</div><div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"htmlfile"</span>:&nbsp;[<span style="color: rgb(163, 21, 21);">"html"</span>,&nbsp;<span style="color: rgb(163, 21, 21);">"htm"</span>,&nbsp;<span style="color: rgb(163, 21, 21);">"tw"</span>]</div><div>&nbsp;&nbsp;&nbsp;&nbsp;},</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"mimetypes"</span>:&nbsp;{</div><div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"text/html"</span>:&nbsp;[<span style="color: rgb(163, 21, 21);">"tw"</span>]</div><div>&nbsp;&nbsp;&nbsp;&nbsp;},</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"mixFolders"</span>:&nbsp;<span style="color: rgb(0, 0, 255);">false</span></div><div>&nbsp;&nbsp;},</div></div></div></div></div></div>

### defaultType: `html` | `json`

The global default directory index format. Default is `html`.

### icons: Hashmap

Hashmap where key is the icon files in `/assets/icons/files` (without the extension) and value is an array of extensions to show the icon for in directory index.

The default is `{ "htmlfile": ["htm", "html"] }`.

Unlike mimetypes, this replaces the default, so htmlfile must be specified as well.

### mimetypes:

Extra extensions to map to certain mime types when serving files.

For example: `{ "text/html": [ "tw" ], "example/other": ["any"] }` adds the .tw and .any extensions.

### mixFolders: boolean

Sort folders separately in directory index or mix them.

## Section `datafolder`

A record of strings which will be added to options.variables object of the TiddlyWiki server instance.

<div style="color: rgb(0, 0, 0); font-family: Menlo, Monaco, &quot;Courier New&quot;, monospace; font-size: 12px; line-height: 18px; white-space: pre; overflow:auto;"><div style="line-height: 18px;"><div style="line-height: 18px;"><div>&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"datafolder"</span>:&nbsp;{</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"root-tiddler"</span>:&nbsp;<span style="color: rgb(163, 21, 21);">"$:/core/save/all-external-js&nbsp;or&nbsp;whatever&nbsp;all&nbsp;your&nbsp;wikis&nbsp;use"</span>,</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"other-tiddlywiki-server-variable"</span>:&nbsp;<span style="color: rgb(163, 21, 21);">"anything&nbsp;tiddlywiki&nbsp;server&nbsp;understands"</span>,</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"incorrect-server-variable"</span>:&nbsp;<span style="color: rgb(163, 21, 21);">"tiddlyserver&nbsp;doesn't&nbsp;check&nbsp;the&nbsp;datafolder&nbsp;object"</span>,</div><div>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: rgb(4, 81, 165);">"spread&nbsp;operator&nbsp;assignment"</span>:&nbsp;<span style="color: rgb(163, 21, 21);">"it&nbsp;just&nbsp;...vars&nbsp;it&nbsp;into&nbsp;the&nbsp;tiddlywiki&nbsp;server&nbsp;variables"</span></div><div>&nbsp;&nbsp;},</div></div></div></div>

One security consideration is that if an object is specified instead of a string for any of the properties, then all data folders will be sharing that object. Changes to the object will be seen by all other data folder instances.

No type checking is done on the values of the datafolder object. They are passed directly to each datafolder instance. Plugins in the data folder can access these variables on the server side using the `"th-server-command-post-start"` hook. The TiddlyWiki Server class from `$:/core/modules/server/server.js` is the first argument in the hook, and the string "tiddlyserver" or "tiddlywiki" is the third argument depending on which environment the data folder is loaded in.

## Section `logging`

The logging options are removed and debugLevel is moved up to the top.