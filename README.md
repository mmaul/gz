NAME: gz

VERSION: .011  

AUTHOR: Mike Maul

AUTHOR_EMAIL: 

PKG_URL: https://github.com/mmaul/gz

DESCRIPTION: Gzip IO interface using zlib

CATEGORY: io compression

LIBDIR: GZ

-----
INSTALLATION
============
Quickstart SetupTool application template for a generic library.

## Quickstart Installation ##
* 'install' must be able to write to Felix INSTALL_ROOT
    scoop install gz

## Manual Installation ##
    scoop get
    cd gz
    flx setup install

Documentation
=============
See GZ/gz.flx

Example
=======
    var fd = open("file.gz",O_RDONLY);
    match gzdopen(fd,Read) with
    |Some ?gzh => { 
      var reader = gzreader(gzh,size(1024));
      while true do
        match (reader()) with
        |GZ_OK (?bytes,?data) => { print$ str(data); } 
        |GZ_NONE => {  goto finish; }
        |GZ_ERR (?code,?s) => { 
          eprintln("Error decompressing stream:"+s); 
          System::exit(-1);  
        }
        endmatch;
      done
    finish:>
      gzclose(gzh);
    }
    |_ => { }
    endmatch;
