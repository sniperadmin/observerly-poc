# Vue 3 + TypeScript + Vite

This template should help get you started developing with Vue 3 and TypeScript in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

Learn more about the recommended Project Setup and IDE Support in the [Vue Docs TypeScript Guide](https://vuejs.org/guide/typescript/overview.html#project-setup).

---

## The Challenge

Integrate the `@unovis` library, along with unocss and `@observerly/astrometry`, to visualise the altitude of the Moon and the Sun graphically.

The requirements are simple, we want a neat and compact graphical user interface for showing the Moon and the Sun during one 24 hour cycle, utilising @unovis.

The style required is Tailwind-esque (using unocss) and must be built with Vue 3 and Typescript.

The UI must be "dark-mode" by default.

## The Astronomy

The Moon and the Sun both rise and set during the 24 hour clock, the maximum altitude either the Moon or Sun could have is 90° and the minimum is -90°.

Astronomical observations are always recorded in UTC.

Plot both the Moon altitude (#2dd4bf, tailwind `bg-teal-500`) against (#93c5fd `bg-blue-300`) using the following time-based functions from `@observerly/astrometry`:

```ts
// For these examples we need to specify a date because most calculations are
// differential w.r.t a time component. We set it to the author's birthday:
export const datetime = new Date('2021-05-14T00:00:00.000+00:00')

// For example we will fix the latitude to be Manua Kea, Hawaii, US
export const latitude = 19.820611

// For example we will fix the longitude to be Manua Kea, Hawaii, US:
export const longitude = -155.468094
```

Thus, we can then use:

```ts
import { convertEquatorialToHorizontal, getSolarEquatorialCoordinate } from '@observerly/astrometry'

const sun = convertEquatorialToHorizontal(
  datetime, 
  { 
    latitude, 
    longitude 
  },
  getSolarEquatorialCoordinate(datetime)
) // returns { alt, az } of the Sun (in degrees) local to the observer at { latitude, longitude }
```

```ts
import { convertEquatorialToHorizontal, getLunarEquatorialCoordinate } from '@observerly/astrometry'

const sun = convertEquatorialToHorizontal(
  datetime, 
  { 
    latitude, 
    longitude 
  },
  getLunarEquatorialCoordinate(datetime)
) // returns { alt, az } of the Moon (in degrees) local to the observer at { latitude, longitude }
```

to get the Solar and Lunar altitudes, accordingly.

## Good Luck

Any questions, please reach out to us.


