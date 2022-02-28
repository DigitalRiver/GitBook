---
description: Learn how to translate the WooCommerce extension.
---

# Translate the extension

Any WordPress plugin including `digitalriver` can be translated to other languages given that the plugin contains a `.POT` file.

### Requirements

* A `.POT` file
* A free version of `POEdit` software.
* WordPress command-line interface (CLI)

### Translation process

Use `POEdit` to open the `.POT` file to create `.po`(Portable Object) file and transform it into `.mo`(Machine Object) files. Here, `.po` is the file created when you translate your POT file to a particular language. For example, `fr_FR.po`. `.MO` is the file that the machine can read, it’s a binary file.&#x20;

Convert your `.po` file to `.mo` file. For example, `fr_FR.mo`.

Consider a scenario where we want to translate this plugin into the Polish language. The Polish language has the locale `pl_PL`

Run the following command from the plugin directory:

```
  npm run language:make-po
```

This will create `pl_PL` directory inside `languages` directory. The`pl_PL` directory would contain different `.po` files, one file for PHP strings and others for JavaScript.

Translate the string in the `.po` file using `poedit` or any other similar software. More information on how you can translate strings using Poedit can be found [here](https://make.wordpress.org/polyglots/handbook/translating/glotpress-translate-wordpress-org/poedit/#:\~:text=Poedit%20is%20an%20open%2Dsource,PO%20file%20and%20.). Once all the strings in `.po` files are translated, run the following command:

```
    npm run language:make-json
```

This will create JSON files that contain JavaScript translations.

**Congratulations!** You have translated the plugin successfully.
