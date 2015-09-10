pynco
============

Language bindings for [NCO](http://nco.sourceforge.net/).  A fork from Ralf Mueller's [cdo-bindings](https://github.com/Try2Code/cdo-bindings).

## `pynco` - Use Python to access the power of [NCO](http://nco.sourceforge.net/)

This package contains the module python `nco`, which implements a python style access to
the [NetCDF Operators (NCO)](http://nco.sourceforge.net/). NCO is a command line tool for processing
netCDF data. Its main focus is climate data, but it can by used for other
purposes too.

## Installation

### Python Installation:

    python setup.py install

### Pypi Installation:

    pip install nco

### Requirements

- [NetCDF Operators (NCO)](http://nco.sourceforge.net/) - Version 4.2 or later
- Python 2.6 or later

**Recommended dependencies for returning `numpy` arrays from `nco` operations**
- [scipy](http://docs.scipy.org/doc/scipy/reference/generated/scipy.io.netcdf.netcdf_file.html)
- [netCDF-4](https://code.google.com/p/netcdf4-python/)
- [numpy](http://www.numpy.org/)

## Usage

#### Importing the Nco class

   `from nco import Nco`

### Run operators

For python an instance has to be created first

    from nco import Nco
    nco = Nco()

Now any NCO command (i.e. ncks, ncra, ...) can be called as a method of `nco`.

* Required argument
   - input - Input netcdf file name, str

* Optional arguments
    - `output` - String or list of strings representing input netCDF filenames.  If not provided and operator returns a file (not an array or stdout text), the method will return a temporary file.
    - `debug` - bool or int, if <0 or True, debug statements will be turned on for NCO and NCOpy (default=False)
    - `returnCdf` - return a netCDF file handle, bool (default=False)
    - `returnArray` - return a numpy array of variable name, str (default='')
    - `returnMaArray` - return a numpy masked array of variable name, str (default='')
    - `return_xray` - return a `xray.Dataset` object, bool (default=False).
    - `options` - a string of NCO input options, for example options='-7 -L 1' (default='')
    - `**kwargs` - any kwarg will be passed as a key, value pair to the nco command `--{key}={value}`.  This allows the user to pass any number of long name commands list in the nco help pages.

### Examples

* File information:

        ncdump_string = nco.ncdump(input=ifile)

* Operators with user defined regular output files:

        nco.ncra(input=ifile, output=ofile)

* Use temporary output files:

        temp_ofile = nco.ncrcat(input=ifile)

* Set global NCO options:

        nco.ncks(input=ifile, output=ofile, options="--netcdf4")

* Return multi-dimension arrrays:

        temperatures = nco.ncra(input=ifile, returnArray=True).variables['T'][:]
        temperatures = nco.ncra(input=ifile, returnCdf=True).variables['T'][:]
        temperatures = nco.ncra(input=ifile, returnArray='T')

## Tempfile helpers

`pynco` includes a simple tempfile wrapper, which makes life easier.  In the
absence of a specified output file, `Nco()` will create a temporary file to allow the results of the task to be returned to the user.  For example:

    temperatures = nco.ncra(input=ifile, returnArray='T')
is equivalent to:

    temperatures = nco.ncra(input=ifile, output=tempfile.mktemp(), returnArray='T')

## Support, Issues, Bugs, ...

Please use the github page for this code: https://github.com/nco/pynco.

## License

`pynco` makes use of the GPLv2 License, see LICENSE.txt.

---

## Other stuff

* Author: Joe Hamman <jhamman1@uw.edu>
* Requires: NCO version 4.2.x or newer, Python 2.6 or later
* Optional: scipy or Python netCDF4
* License:  Copyright 2015 by Joe Hamman.  Released under GPLv2 license.  See the LICENSE file included in the distribution.
