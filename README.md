# dropdown

> Custom dropdown component for Vue2.js. Accepts an array of strings, an array of objects with a definable display key, or a sectioned group of arrays also with defined section titles and display keys.

```html

Standard Dropdown:

<dropdown
    :data="dropdownItems"
    :display-key="'label'"
    :current-selection="'Please select'"
    @update="alertDogScore($event)" />

    given data:
    dropdownItems: [
        { label: 'Corgi', value: 1000 },
        { label: 'Australian Shepard', value: 950 },
        { label: 'Beagle', value: 900 },
        { label: 'Labrador', value: 750 },
        { label: 'Goldendoodle', value: 600 }
    ]

Sectioned Dropdown:

<dropdown
    :sections="sectionedDropdownItems"
    :display-key="'name'"
    :current-selection="sectionedDropdownItems[1].data[2].name"
    @update="alertNameScore($event)" />

    given data:
    sectionedDropdownItems: [
        {
            sectionTitle: 'Girl Names',
            data: [
                { value: 100, name: 'Susie' },
                { value: 200, name: 'Debbie' },
                { value: 50, name: 'Patricia' }
            ]
        },
        {
            sectionTitle: 'Boys',
            data: [
                { value: 100, name: 'John' },
                { value: 200, name: 'Steve' },
                { value: 50, name: 'Harry' }
            ]
        }
    ]

```

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
