---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
#background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: "text-center"
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS
css: unocss
---

# volto-react-table-widget

A widget to replace the accordions at ObjectListWidget

---

# Scenario

- A usecase where we need datagridfield
- Just add a JSONField to the schema
- And configure the ObjectListWidget in the frontend

```js
const applyConfig = (config) => {
  config.widgets.widget = {
    ...config.widgets.widget,
    bounding_widget: BoundingWidget,
  };
  return config;
};
```

---

```jsx
import ObjectListWidget from '@plone/volto/components/manage/Widgets/ObjectListWidget';

const ItemSchema = {
  title: 'Bounding-box',
  properties: {
    west: {
      title: 'West',
      description: 'West side Longitude, between -180 and 180',
      type: 'number',
    },
    east: {
      title: 'East',
      description: 'East side Longitude, between -180 and 180',
      type: 'number',
    },
    north: {
      title: 'North',
      description: 'North side Latitude, between -90 and 90',
      type: 'number',
    },
    south: {
      title: 'South',
      description: 'South side Latitude, between -90 and 90',
      type: 'number',
    },
  },

```

---

```jsx
  fieldsets: [
    {
      id: 'default',
      title: 'Bounding-Box',
      fields: ['east', 'west', 'north', 'south'],
    },
  ],
  required: [],
};

const BoundingWidget = (props) => {
  return (
    <ObjectListWidget
      schema={ItemSchema}
      {...props}
      value={props.value?.items || props.default?.items || []}
      onChange={(id, value) => props.onChange(id, { items: value })}
    />
  );
};
```

---

# Easy!

<video class="video-js" data-setup="{}" controls preload="auto" width="640px" height="480px">
  <source src="/1-fast.mp4" />
</video>

---

# But...

- What if the user needs 1000 rows there?
- Those accordions are not performant at all
- The browser dies
- We need a solution

---

# What if we use react-table?

- Now called TanStack table
- Lightweight
- Ton of options:
  - Pagination
  - Hide/show columns
  - Filters
  - Search
  - Sorting
  - ...
- Really fast

---

# volto-react-table-widget

- Add `@eeacms/volto-react-table-widget` to your package.json dependencies and addons.
- Configure it like the ObjectListWidget

```js
const applyConfig = (config) => {
  config.widgets.widget = {
    ...config.widgets.widget,
    downloadable_files_widget: DownloadableFilesTableWidget,
  };
  return config;
};
```

---

```jsx
import React from 'react';
import { ReactTableWidget } from '@eeacms/volto-react-table-widget';

const ItemSchema = () => ({
  title: 'Downloadable File',
  properties: {
    title: {
      title: 'Title',
      description: 'Enter the title of this file.',
      type: 'string',
    },
    file: {
      title: 'File name',
      description: 'Enter the file name.',
      type: 'string',
    },
    area: {
      title: 'Area of interest',
      description: 'Enter the area of this file.',
      type: 'string',
    },
    year: {
      title: 'Year',
      description: 'Enter the year of this file.',
      type: 'number',
      minimum: 1900,
    },
    version: {
      title: 'Version',
      description: 'Enter the version of this file.',
      type: 'string',
    },
    resolution: {
      title: 'Resolution',
      description: 'Enter the resolution of this file. Ex.: 100m',
      type: 'string',
    },
    type: {
      title: 'Type',
      description: 'Enter the file type of this file. Ex.: Raster or Vector',
      choices: [
        ['Raster', 'Raster'],
        ['Vector', 'Vector'],
      ],
    },
    format: {
      title: 'Format',
      description: 'Enter the format of this file.',
      type: 'string',
    },
    size: {
      title: 'Size',
      description: 'Enter the size of this file. Ex.: 3.5 GB',
      type: 'string',
    },
    path: {
      title: 'Path',
      description: 'Enter the absolute path of this file in the storage',
      type: 'string',
    },
    source: {
      title: 'Source',
      description: 'Enter the source of this file (this is an internal).',
      choices: [
        ['EEA', 'EEA'],
        ['HOTSPOTS', 'HOTSPOTS'],
      ],
    },
  },
```

---

```jsx
  fieldsets: [
    {
      id: 'default',
      title: 'File',
      fields: [
        'title',
        'file',
        'area',
        'year',
        'version',
        'resolution',
        'type',
        'format',
        'size',
        'path',
        'source',
      ],
    },
  ],
  required: [],
});
```

---

```jsx
const DownloadableFilesTableWidget = (props) => {
  return (
    <ReactTableWidget
      schema={ItemSchema()}
      {...props}
      csvexport={true}
      csvimport={true}
      value={props.value?.items || props.default?.items || []}
      onChange={(id, value) => props.onChange(id, { items: value })}
    />
  );
};

export default DownloadableFilesTableWidget;
```

---

# Pagination and inline edit

<video class="video-js" data-setup="{}" controls preload="auto">
  <source src="/2-fast.mp4" />
</video>

---

# Add/Remove new items

<video class="video-js" data-setup="{}" controls preload="auto">
  <source src="/3-fast.mp4" />
</video>
---

# Bonus point!

- CSV export/import
- react-papaparse

---

# CSV import/export

<video class="video-js" data-setup="{}" controls preload="auto">
  <source src="/4-fast.mp4" />
</video>

---

# Check it

@eeacms/volto-react-table-widget

https://github.com/eea/volto-react-table-widget

---
