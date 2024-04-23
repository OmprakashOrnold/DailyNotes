# Install Bootstrap Locally in an Angular Project

## Prerequisites
* You should already have an existing Angular project

## Install Bootstrap

1. Open a terminal window and move to your Angular project directory

2. Install the Bootstrap files with the following command:

    ```
    npm install --save bootstrap jquery
    ```

   This command actually installs Bootstrap and jQuery. We are adding jQuery in case you need to use some of the Bootstrap+jQuery functionality in the future.

   The `--save` flag will save the files in the `node_modules` directory. The final location for the Bootstrap CSS file will be 

   ```
   node_modules/bootstrap/dist/css/bootstrap.min.css
   ```

2. In a text editor, open the file in your project directory: `angular.json`

3. In the `angular.json` file, move to the `styles` section.

    a. Add a new entry for Bootstrap CSS file

    ```
        "styles": [
            "src/styles.css",
            "node_modules/bootstrap/dist/css/bootstrap.min.css"
        ],
    }
    ```

4. In the `angular.json` file, move to the `scripts` section.

    a. Add a new entry for jQuery and Bootstrap JavaScript files

    ```
    "scripts": [
        "node_modules/jquery/dist/jquery.min.js",
        "node_modules/bootstrap/dist/js/bootstrap.min.js"
    ]
    ```
5. If your Angular app is running, be sure to stop and restart it. This is required in order to pick up the new configurations in the `angular.json` file.

That's it! You have successfully installed Bootstrap locally in your Angular project.

---
