# webdav-fs
Node fs wrapper for WebDAV.

[![Build Status](https://travis-ci.org/perry-mitchell/webdav-fs.svg)](https://travis-ci.org/perry-mitchell/webdav-fs)

## Installation

Install webdav-fs using npm:

```
npm install webdav-fs --save
```

## Example

You can use webdav-fs in authenticated or non-authenticated mode:

```
// Using authentication:
var wfs = require("webdav-fs")(
		"http://example.com/webdav/",
		"username",
		"password"
	);

wfs.readdir("/Work", function(err, contents) {
	if (!err) {
		console.log("Dir contents:", contents);
	} else {
		console.log("Error:", err.message);
	}
});
```

```
// Without using authentication:
var wfs = require("webdav-fs")("http://example.com/webdav/");

wfs.stat("/report.docx", function(err, data) {
	console.log("Is file:", data.isFile());
});
```

## API

The following methods are available on the `webdav-fs` module:

### readdir(path, callback)

Read the contents of a remote directory:

```
wfs.readdir("/some/remote/path/", function(error, contents) {
	// callback is an array of filenames
});
```

### readFile(path, [encoding,] callback)

Read the contents of a remote file:

```
wfs.readFile("/website/index.php", "utf8", function(error, data) {
	// data is the contents of the file
	// encoding is optional
});
```

### stat(path, callback)

Stat a remote file:

```
wfs.stat("/the-internet.dat", function(error, fileStat) {
	console.log(fileStat);
});
```

A stat has the following properties:

| Property | Type | Description |
| -------- | ---- | ----------- |
| isFile   | Function | Check if the item is a file |
| isDirectory | Function | Check if the item is a directory |
| mtime | Number | Last modification timestamp |

### writeFile(path, data, [encoding,] callback)

Write data to a remote file:

```
wfs.writeFile("/Temp/im-here.txt", "This is a saved file! REALLY!!", function(err) {
	console.error(err.message);
});
```
