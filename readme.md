# easyeda2kicad.py

A Python script that convert any electronic components from [EasyEDA](https://easyeda.com/) or [LCSC](https://www.lcsc.com/) to a Kicad library

<p align="center">
  <img src="https://raw.githubusercontent.com/uPesy/easyeda2kicad.py/master/ressources/demo_symbol.png" width="500">
</p>
<div align="center">
  <img src="https://raw.githubusercontent.com/uPesy/easyeda2kicad.py/master/ressources/demo_footprint.png" width="500">
</div>


## Installation

```bash
pip install easyeda2kicad
```
The script uses only one external library [pydantic](https://pydantic-docs.helpmanual.io/) for data validation.

## Usage

```bash
# For symbol + footprint
easyeda2kicad --symbol --footprint --lcsc_id=C2040
# For symbol only
easyeda2kicad --symbol --lcsc_id=C2040
# For footprint only
easyeda2kicad --footprint --lcsc_id=C2040
```

By default, all librairies are saved in `C:/Users/your_name/Documents/Kicad/easyeda2kicad/`, with :
- `easyeda2kicad.lib` for symbol library
- `easyeda2kicad.pretty/` for footprint libraries

If you want to save components symbol/footprint in your own libs, you can specify the output lib path by using `--output` option.

```bash
easyeda2kicad --symbol --footprint --lcsc_id=C2040 --output ~/libs/my_lib
```

This command will save:
- the symbol in `~/libs/my_lib.lib` file for symbol library. The file will be created if it doesn't exist
- the footprint in `~/libs/my_lib.pretty/` folder for footprint libraries. The folder will be created if it doesn't exist

You can use the option `--overwrite` to update a component symbol/footprint that is already in a Kicad library (generated by easyeda2kicad)

```bash
easyeda2kicad --symbol --footprint --lcsc_id=C2040 --output ~/libs/my_lib --overwrite
```

## Add libraries in Kicad

**These are the instructions to add the default easyeda2kicad libraries in Kicad.**
Before configuring KiCad, run at least once time the script to create lib files. For example :

```bash
easyeda2kicad --symbol --footprint --lcsc_id=C2040
```

- In KiCad, Go to Preferences > Configure Paths, and add the environment variables `EASYEDA2KICAD` :
  - Windows : `C:/Users/your_username/Documents/Kicad/easyeda2kicad/`,
  - Linux : `/home/your_username/Documents/Kicad/easyeda2kicad/`
- Go to Preferences > Manage Symbol Libraries, and Add the global library `easyeda2kicad` : `${EASYEDA2KICAD}/easyeda2kicad.lib`
- Go to Preferences > Manage Footprint Libraries, and Add the global library `easyeda2kicad` : `${EASYEDA2KICAD}/easyeda2kicad.pretty`
- Enjoy :wink:

## Notes

**It's still in development : all features are not implemented. I'm not a Python expert and don't have a lot of free time for coding.
Feel free to contribute :slightly_smiling_face:**

Some stuffs to be done:
- [ ] Add unit testing and code coverage badge


## Inspirations

- [KiPart](https://github.com/devbisme/KiPart) - A utility that generates single
and multi-unit symbols from a CSV file containing all the pin information for
one or more parts.
