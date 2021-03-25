# PyBuilder setup.cfg plugin

[PyBuilder](http://pybuilder.github.io/) plugin for getting various information from the setup.cfg file.

## How to use it

In your `build.py`:

```
use_plugin("pypi:pybuilder_setup_cfg")
```

**IMPORTANT** Use this plugin as the first one as it's getting basic data from the `setup.cfg` that may be overwritten/adjusted later on. It may not work properly if not loaded as the first plugin in your project.

The setup_cfg plugin works as an initializer. You do not have to do anything else. 

It reads the following settings from the setup.cfg file (or from environment variables) and set project properties accordingly:
- **PROPERTY_NAME ($ENV_VAR_NAME _if applicable_, [SECTION_IN_SETUP_CFG].OPTION)**
- name
  - envvar: PYB_SCFG_NAME
  - section: metadata
  - option: name
- version
    - envvar: PYB_SCFG_VERSION
    - section: metadata
    - option: name
- package_data
    - section: options.package_data (standard location)
      
        OR

    - section: files
    - option: package_data
    - description: list of items where each item is a whitespace or comma separated list of file patterns to include
- default_task
    - section: tool:pybuilder
    - option: default_task
    - description: list of default task names
- distutils_commands
    - envvar: PYB_SCFG_DISTUTILS_COMMANDS
    - section: tool:pybuilder
    - option: distutils_commands
    - description: list of distutils commands to execute
- distutils_upload_repository 
    - envvar: PYB_SCFG_UPLOAD_REPOSITORY
    - section: tool:pybuilder
    - option: distutils_upload_repository
    - note: if environment variable `TWINE_REPOSITORY_URL` is set, it will be used anyway and the `distutils_upload_repository` will be ignored
- distutils_cython_ext_modules (*)
    - section: tool:pybuilder
    - option: cython_include_modules AND cython_exclude_modules
    - description: lists of file patterns
- distutils_cython_remove_python_sources (*)
    - section: tool:pybuilder
    - option: cython_remove_python_sources
- copy_resources_glob
    - section: tool:pybuilder
    - option: copy_resources_glob
    - note: it's adding files from _package_data_ automatically
- pytest_coverage_break_build_threshold
    - envvar: PYB_SCFG_PYTEST_COVERAGE_BREAK_BUILD_THRESHOLD
    - section: tool:pytest
    - option: coverage_break_build_threshold
- pytest_coverage_html
    - section: tool:pytest
    - option: coverage_html
- pytest_coverage_annotate
    - section: tool:pytest
    - option: coverage_annotate

(*) Cython-related stuff is not integrated in official PyBuilder, there is a PR [#640](https://github.com/pybuilder/pybuilder/pull/640) for that.