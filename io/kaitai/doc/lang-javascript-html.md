Kaitai Struct: JavaScript notes
==========

Quick start
----------

### Node.js ###

Create an empty directory and install the [runtime from npm](https://www.npmjs.com/package/kaitai-struct) by running:

```
npm i kaitai-struct
```

Copy your compiled .ksy parser into this directory or download one [parser from the format gallery](//formats.kaitai.io/) (eg. [Elf.js](//formats.kaitai.io/elf/javascript.html)).

Create `index.js` with the following content:

```
const fs = require("fs");
const Elf = require("./Elf");
const KaitaiStream = require('kaitai-struct/KaitaiStream');

const fileContent = fs.readFileSync("/bin/ls");
const parsedElf = new Elf(new KaitaiStream(fileContent));
console.log(parsedElf);
```

Test the code by running `node index.js`.

### Browser ###

Create an `index.html` with the following content:

```
<html>
<head>
    <script src="KaitaiStream.js"></script>
    <script src="Elf.js"></script>
</head>
<body>
    <pre id="dump">parsing in process...</pre>
    <script>
        var oReq = new XMLHttpRequest();
        oReq.open("GET", "sample.elf", true);
        oReq.responseType = "arraybuffer";

        oReq.onload = function (oEvent) {
            var arrayBuffer = oReq.response;
            var parsedElf = new Elf(new KaitaiStream(arrayBuffer));
            document.getElementById("dump").textContent =
                "machineType: " + Elf.Machine[parsedElf.header.machine] + "\n" +
                "program headers:\n" + parsedElf.header.sectionHeaders.map(x => " - " + x.name).join("\n");
        };

        oReq.send(null);
    </script>
</body>
</html>
```

Copy your compiled .ksy parser into this directory or download one [parser from the format gallery](//formats.kaitai.io/) (eg. [Elf.js](//formats.kaitai.io/elf/javascript.html)).

Also deploy the Kaitai Struct JavaScript Runtime (`KaitaiStream.js`) [from Github](https://github.com/koczkatamas/kaitai_struct_javascript_runtime/blob/master/KaitaiStream.js) or [npm](https://www.npmjs.com/package/kaitai-struct) and a `sample.elf` file.

Publish the files on a webserver. Simplest method is running `python -mSimpleHTTPServer` and opening <http://localhost:8000>.

Approximate 64-bit integers
----------

Current JavaScript specification lacks direct access to anything like
int64 type. Instead, accessing long integers would automatically
represent them internally as double-precision IEEE754 floats, potentially
losing least significant bits. It should be ok for smaller integers (up
to 53 significant bits), but note that JavaScript would use approximate
values for everything beyond that.
