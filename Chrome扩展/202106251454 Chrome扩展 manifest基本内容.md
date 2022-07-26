```

{
    "manifest_version": 2,
    "name": "popup extension",
    "version": "0.2",
    "description": "Build an Extension!",
    "content_scripts": [
        {
            "matches": [
                "<all_urls>"
            ],
            "js": [
                "content.js"
            ]
        }
    ],
    "background": {
        "service_worker":"background.js"
    },
   
    "permissions": [
        "tabs"
      ],

       "browser_action": {
        "default_icon": 
            "wt.png",
            "default_popup": "sketch/index.html",
            "default_title":"A popup will come here."
         
    }
}

```