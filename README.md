# TeapotDome

This is an experiment in using software development processes like 
[_source control_](https://en.wikipedia.org/wiki/Version_control) and a 
[_one step build_](http://www.joelonsoftware.com/articles/fog0000000043.html) 
for a seismic interpretation project.

Check out the build output for the [2D survey map](./2DNavigationLinesA-E.geojson).

## Getting started

You can run this experiment on your own machine, or a cloud development environment.

### Cloud Environment

- [Clone in Cloud9](https://c9.io/auth/github?r=https://c9.io/open/?clone_url=git@github.com:softwareunderground/TeapotDome.git)
- In the terminal run:

```
npm install
jake
```

### Local Environment

You need the following tools installed:

- [git](https://git-scm.com)
- [git-lfs](https://git-lfs.github.com)
- [node](https://nodejs.org) (including [npm](https://www.npmjs.com))

#### Clone the repo, install dependencies and build

From the command line:
    
    git clone https://github.com/softwareunderground/TeapotDome.git
    cd TeapotDome
    npm install
    npm run build

## Observation

After cloning, observe that files that represent source field data are inside the `source` directory.  While code and byproducts are outside of that directory.

Try changing X and Y values in `/source/2D_Seismic/2DNavigationLinesA-E.txt`.
Then run `npm run build` again (or just `jake` if on Cloud9). Observe that the GEOjson was regenerated. (Hint: use `git diff`.)
Then, run the build a second time without making changes. Observe that the build did not need to update the GEOjson file.

The idea is that dependent data can be updated in a single step when new input data is updated. (Doing this in an even more automatic fashion is called [Build Automation](https://en.wikipedia.org/wiki/Build_automation).)

## Attribution

Teapot Dome data being used to demonstrate this process is
courtesy of 
[RMOTC](http://www.fe.doe.gov/facilities/rmotc/) and the U.S. Department of Energy.

This experiment was started at the 
[2015 Geophysics Hackathon](http://www.agilegeoscience.com/events/2015/10/17/geophysics-hackathon-2015).

## Notes

### LFS

Looking at [.gitattributes](./.gitattributes) you see that SEG-Y files are associated with 
[git Large File Storage](https://git-lfs.github.com). 
This was accomplished with the following command:

`git lfs track "*.sgy" "*.segy"`

The 3D survey is not yet in this repo because GitHub restricts even large files to 100MB.

### GIS

From [2DNavigationLinesA-E.txt](./source/2D_Seismic/2DNavigationLinesA-E.txt) we find that the XY values
are in the [NAD27 State Plane for Wyoming East Central](https://epsg.io/32056). 

The build generates a [geoJSON file GitHub can easily display](https://help.github.com/articles/mapping-geojson-files-on-github/)
converted to [WGS84](https://epsg.io/4326) degrees.

Using [EarthPoint.us](http://www.earthpoint.us/StatePlane.aspx) we can check a conversion. We expect something like: 
804635, 935826 -> 42.1527484°, -109.2056781°.
