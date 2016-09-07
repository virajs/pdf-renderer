# Pdf renderer

# Install

```
npm i
```

#Start

```
npm start
```

post html content to `/pdf` to receive a rendered pdf


#Configuration Variables

server is running on `PORT`

#TODO

save generated pdf files to tmp instead of `./files`

#How to use

####With curl

```
curl -X POST -H "Cache-Control: no-cache" -d '<html>
<body><h1>Hello</h1></body>
</html>' "http://localhost:8080/pdf"
```

####With nodejs

```javascript
var http = require("http");

var options = {
  "method": "POST",
  "hostname": "localhost",
  "port": "8080",
  "path": "/pdf",
  "headers": {
    "cache-control": "no-cache"
  }
};

var req = http.request(options, function (res) {
  var chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function () {
    var body = Buffer.concat(chunks);
    console.log(body.toString());
  });
});

req.write("<html>\n<body><h1>Hello</h1></body>\n</html>");
req.end();
```

# Jenkins - CD
## build variables
`pdf_renderer_port: "3020"`

Build Pipeline: cromwell-pdf-renderer-pipeline
