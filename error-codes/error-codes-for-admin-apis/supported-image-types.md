---
description: Understand the supported image types.
---

# Supported image types

## Defining a file&#x20;

To define a file to import, the attribute file must start with `file:` **** and end with file ID. For example:

* With JSON, "productImage1": "file:00fb210-12345678", Global Commerce imports file 00fb210-12345678 and places it into a default folder of product detail images for the given company.

## Creating subfolders

To create a subfolder, add the `file:` prefix to the subfolder path and the `fileID`. For example:

* With JSON, `"thumbnailImage2": "file:folderA/folderB/00fb210-12345678"`, Global Commerce creates the subfolders '`folderA`' and '`folderB`' in the product thumbnail image folder for the given company. File `00fb210-12345678` is imported into the folders. &#x20;
* Subfolders can start with a **/** or not. For example, `file:abc` **** is the equivalent to `file:/abc`.&#x20;
* More than one **/** will be treated the same as one. For example, `file:////abc////def` **** is equivalent to `file:abc/def`.&#x20;

Error codes related to file types have the prefix '`attribute_external_file`'. Refer to [Admin API error codes](./) for more details.

## Image type attributes &#x20;

* Product details images&#x20;
* Product thumbnail images&#x20;
* Custom attributes with image types&#x20;

Global Commerce requires images to be of certain image types. The only supported image types are:

* JPG, JPEG, GIF, BMP, and WEBP.&#x20;
  * The file extension must match the image type.
  * The file content must match the file extension.

Both the file name (excluding the file extension) and folder do not support special characters. The special characters are:&#x20;

* &#x20;**! \ < > / | ? \* : ' " . ( ) & ^ \~  #  % { } , @ + = \` ; \[ ]**, as well as spaces, tab \t, breakline \r \n \f.&#x20;

## File type attributes

* padFile of software family&#x20;
* custom attributes with file types&#x20;
* cannot have subfolders at the product level &#x20;
* Any file type is supported&#x20;
* If the file type is .zip, Global Commerce checks all the files zipped within.&#x20;
* .File names do not support special characters. The special characters are:
  * &#x20;**| ; , ! @ $ ( ) < > " ' \` \~ { } \[ ] = + &  ^ %** and spaces.&#x20;
