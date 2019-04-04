# Ceedling-ModuleCreate-Example

This repository was created as an example of a feature of Ceedling-Unity.

With a modification of the module generator of Unity, its posible to use boilerplate files as templates for newly created modules.

## Descrtiption of the repositorty

A posible folder structure is shown in the next snippet
```bash
.
├── boilerplates
├── exampleProject
├── third-party
└── tools
```
but it can be structured like the following
```bash
.
├── boilerplates
├── build
├── doc
├── source
├── third-party
└── tools
```
At the moment, the boilerplates folder is located at the root but it can be moved to /tools for a more suited place.

The main elements are the *source* folder, where our code will be located, the *build* folder where the artifacts and other intermediate files will be created, and the supporting elements of _tools_, _third-party_, etc.

Our code can be organized in modules, intialy created with ceedling within the *source* folder. To do this automatically and according with template files, we can use the *module generator* feature of Unity.

## Boilerplates
As a starting point for our yet to be created module files we can use a template determined by us or the organization in wich we work.

For example we can see the [header template file](/tools/ceedling/template/moduleUnderTest/inc/module.h) for the GICSAFe organization:
```C
/*
 *  --------------------------------------------------------------------------
 *
 *                               GICSAFe-Firmware
 *                               ----------------
 *
 *                      Copyright (C) 2019 CONICET-GICSAFe
 *          All rights reserved. Protected by international copyright laws.
 *
 *  Contact information:
 *  site: https://github.com/gicsafe-firmware
 *  e-mail: <someone>@<somewhere>
 *  ---------------------------------------------------------------------------
 */

/**
 *  \file   module.h
 *  \brief  Specifies this module.
 */

/* -------------------------- Development history -------------------------- */
/*
 */

/* -------------------------------- Authors -------------------------------- */
/*
 *  RiGr  Rick Grimes  rick.grimes@twd.com
 */

/* --------------------------------- Notes --------------------------------- */
/* --------------------------------- Module -------------------------------- */
#ifndef __MODULE_H__
#define __MODULE_H__

/* ----------------------------- Include files ----------------------------- */
/* ---------------------- External C language linkage ---------------------- */
#ifdef __cplusplus
extern "C" {
#endif

/* --------------------------------- Macros -------------------------------- */
/* -------------------------------- Constants ------------------------------ */
/* ------------------------------- Data types ------------------------------ */
/* -------------------------- External variables --------------------------- */
/* -------------------------- Function prototypes -------------------------- */
/* -------------------- External C language linkage end -------------------- */
#ifdef __cplusplus
}
#endif

/* ------------------------------ Module end ------------------------------- */
#endif

/* ------------------------------ End of file ------------------------------ */

```

To adapt the template and create the boilerplate, we only need to replace the ocurrences of:
1. the *name* of the module (in this case the word "module" itself) for the string *"%1$s"*,
2. the lists of common included header files for *"%2$s"* (In this case there was none, but de argument can be inserted in the "Include files" section to comply with the template),
3. and finally the *name* again but in *CAPS* for *"%3$s"*.

This process results in a [file](boilerplates/ceedlingModule/module.h) like this:
```C
/*
 *  --------------------------------------------------------------------------
 *
 *                               GICSAFe-Firmware
 *                               ----------------
 *
 *                      Copyright (C) 2019 CONICET-GICSAFe
 *          All rights reserved. Protected by international copyright laws.
 *
 *  Contact information:
 *  site: https://github.com/gicsafe-firmware
 *  e-mail: <someone>@<somewhere>
 *  ---------------------------------------------------------------------------
 */

/**
 *  \file   %1$s.h
 *  \brief  Specifies this module.
 */

/* -------------------------- Development history -------------------------- */
/*
 */

/* -------------------------------- Authors -------------------------------- */
/*
 *  RiGr  Rick Grimes  rick.grimes@twd.com
 */

/* --------------------------------- Notes --------------------------------- */
/* --------------------------------- Module -------------------------------- */
#ifndef __%3$s_H__
#define __%3$s_H__

/* ----------------------------- Include files ----------------------------- */
%2$s/* ---------------------- External C language linkage ---------------------- */
#ifdef __cplusplus
extern "C" {
#endif

/* --------------------------------- Macros -------------------------------- */
/* -------------------------------- Constants ------------------------------ */
/* ------------------------------- Data types ------------------------------ */
/* -------------------------- External variables --------------------------- */
/* -------------------------- Function prototypes -------------------------- */
/* -------------------- External C language linkage end -------------------- */
#ifdef __cplusplus
}
#endif

/* ------------------------------ Module end ------------------------------- */
#endif

/* ------------------------------ End of file ------------------------------ */

```

## Usage

### Creating a new Module
To create a new module we can navigate to our source folder, where the *proyect.yml* is located and execute:
```bash
$ ceedling module:create[newModule:newModule]
```

The following files will be created:
```bash
.
├── newModule
│   ├── inc
│   │   └── newModule.h
│   ├── src
│   │   └── newModule.c
│   └── test
│       └── test_newModule.c
└── project.yml
```

### Running tests
To run the test, we can simply call:
```bash
$ ceedling test:all
```
executing the test of all modules.

Or we can call for the execution of the test of a single module with:
```bash
$ ceedling test:singleModuleName
```

All the intermediate files and artifacts will be out of the source folder, in build.
