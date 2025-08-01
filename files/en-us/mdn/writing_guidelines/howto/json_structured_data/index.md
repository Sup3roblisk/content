---
title: How to use structured data
short-title: Use structured data
slug: MDN/Writing_guidelines/Howto/JSON_Structured_data
page-type: mdn-writing-guide
sidebar: mdnsidebar
---

MDN stores data in well-defined structures when possible. This information is then centralized and can be updated once, while being used in numerous places.

There are several such files, and this document describes their purpose, structure, and maintenance process.

## GroupData: logical grouping of APIs

`GroupData` is a JSON file collecting information about Web APIs. The grouping of APIs is somewhat fuzzy: any interface, method or property can be part of several APIs. The set of APIs grouped under a name is a convention used to communicate about a feature, without any technical enforcement.

Yet, MDN needs this information to create coherent Web-API sidebars (like with the `\{{APIRef}}` macro) with the proper reference pages, guides, and overview articles.

GroupData does exactly that: for each API, it lists the interfaces, properties, methods, guides, and overview pages. In the past, it also listed dictionaries and callbacks. But that use, though still supported, is deprecated and will be removed in the future.

### Structure of GroupData

> [!WARNING]
> Non-existent pages listed in this file are ignored (in en-US).

An entry in `GroupData.json` has the following structure:

```json
"Name_of_the_API": {
  "overview": ["name_of_the_overview_page"],
  "guides": [
    "name_of_guide_1",
    (…)
  ],
  "interfaces": [
    "name_of_interface_1",
    (…)
  ],
  "methods": [
    "name_of_additional_method_1",
    (…)
  ],
  "properties": [
    "name_of_additional_property_1",
    (…)
  ],
  "events": [
    "name_of_additional_property_1",
    (…)
  ]
}
```

…where:

- `"Name_of_the_API"`
  - : This key is both an ID used by sidebar macros like `\{{APIRef("Name_of_the_API")}}` and the name displayed in the sidebar itself. Choose it wisely.
    > [!WARNING]
    > If you want to change the name displayed in the sidebar, you must edit all the pages displaying it.
- `"overview"`
  - : This is a list containing one page: the overview page, used as the link for the `"Name_of_the_API"` text. The value is the _title of the page_, and the page must be in the `web/api/` directory.
- `"guides"`
  - : This is a list of guides to display in the sidebar, in the given order. The values are _paths to the page_, starting with `/docs/`.
- `"interfaces"`
  - : This lists the interfaces that are part of the API.
- `"methods"`
  - : This lists the methods that are part of the API.
    > [!NOTE]
    > The methods of the interfaces listed in `"interfaces"` **must** not be listed there. They are automatically added to the sidebar if the `page-type` key for that page is `web-api-static-method` or `web-api-instance-method`.
- `"properties"`
  - : This lists the properties on other interfaces that are part of the API, like `navigator.xr` (a property that the WebXR API adds to the `navigator` object)
    > [!NOTE]
    > The properties of the interfaces listed in `"interfaces"` **must** not be listed there. They are automatically added to the sidebar if the `page-type` key for that page is `web-api-static-property` or `web-api-instance-property`.
- `"events"`
  - : This lists events of other interfaces that are part of the API. The values are the _title of the pages_.
    > [!NOTE]
    > The events targeting the interfaces listed in `"interfaces"` **must** not be listed there. They are automatically added to the sidebar if the `page-type` key for that page is `web-api-event`.

There are two other keys, `"dictionaries"` and `"callbacks"`, operating on the same principle. As we no longer document these entities in their own pages, their use is deprecated, and no new entry should be added to them (and we remove them little by little).

> [!NOTE]
> Also, none of the keys are mandatory; it is good practice (and we'll enforce this) to add the non-deprecated ones with an empty list rather than omitting them. It shows that the absence of value is a conscious choice.

### Update process for GroupData

This file, located at [`files/jsondata/GroupData.json`](https://github.com/mdn/content/blob/main/files/jsondata/GroupData.json), should be updated in the same PR where changes affecting the sidebar happens. That way, the sidebar is always up-to-date. Reviewers shouldn't merge PRs that don't adopt it.

To test your changes, check that the sidebar in the files in your PR displays all entries correctly.

## InterfaceData: recording interface inheritance

> [!NOTE]
> We hope to generate this file automatically from the data available via w3c/webref in the future.

`InterfaceData` describes the hierarchy of the interfaces. It lists inheritance. In the past, it also listed mixins implemented by each interface; but that usage is deprecated, and we remove mixins from this file at the same rate MDN is updated.

This inheritance data is used when building API sidebars and by the `\{{InheritanceDiagram}}` in the interface pages.

### Structure of InterfaceData

An entry in `InterfaceData.json` has the following structure:

```json
"Name_of_the_interface": {
  "inh": "Name_of_the_parent_interface",
  "impl": []
}
```

> [!NOTE]
> As mixins are deprecated, `"impl"` must be an empty list for all new interfaces.

The value of `"Name_of_the_parent_interface"` is not a list but a single entry, mandatory; we must not list any interface that don't inherit from another one.

### Update process for InterfaceData

The same PR adding a new interface that inherits from another one must update this file, located at [`files/jsondata/InterfaceData.json`](https://github.com/mdn/content/blob/main/files/jsondata/InterfaceData.json). Reviewers shouldn't merge PRs that don't do so.

To test your changes, check that the sidebars of each interface you edited in your PR display inheritance correctly.

## SpecData: Specification information

> [!WARNING]
> The [`SpecData.json`](https://github.com/mdn/content/blob/main/files/jsondata/SpecData.json) file is no longer maintained.
> Canonical specification information is stored at [w3c/browser-specs](https://github.com/w3c/browser-specs) and in the `spec_url` key of features defined at [mdn/browser-compat-data](https://github.com/mdn/browser-compat-data).

We do not accept any further contributions to the `SpecData.json` file; instead, insert a specification table using the `\{{Specifications}}` macro, or link to the specification in prose.
Note that most of the time, mentioning or linking to a specification outside the _Specifications_ section is a sign of something not appropriately documented on MDN.
