# ipp-browser

IPP-browser is a powerful library that brings the power of Internet Printing Protocol (IPP) directly into the browser.
Inspired by the work of [William Kapke](https:///github.com/williamkapke/ipp), this library extends the use of IPP to the browser.
With this library, you can easily integrate printing to IPP-compatible network devices directly from your web applications without having to rely on additional plugins or software.

## Installation

​

#### npm

```sh
$ npm install ipp-browser --save
```

​

#### yarn

```sh
$ yarn add ipp-browser
```

​

## API

​
​

### Printer(url [,options])

To interact with a printer, create a `Printer` object.
​
**options:**

- `charset` - Specifies the value for the 'attributes-charset' attribute of requests. Defaults to `utf-8`.
- `language` - Specifies the value for the 'attributes-natural-language' attribute of requests. Defaults to `en-us`.
- `uri` - Specifies the value for the 'printer-uri' attribute of requests. Defaults to `ipp://+url.host+url.path`.
- `version` - Specifies the value for the 'version' attribute of requests. Defaults to `2.0`.
  ​
  ​

### Printer.encodeMsg(operation, msg)

Converts an IPP message object to IPP binary.
​

- 'operation' - There are many operations defined by IPP. See: [/lib/types.ts](https://github.com/adelantsoftware/ipp-browser/blob/main/lib/types.ts#L1).
- 'message - A javascript object to be serealized into an IPP binary message.
  ​
  ​

### Printer.getHeaders(headers?)

Returns the heades to be included in your request
​

- 'headers' - The headers you want to add to the request.
  ​
  ​

## Usage/Example

#### Create a print request

​

```javascript
import Printer from '@adelant/ipp-browser';
import axios from 'axios';
​
let url ="http://192.168.x.y:631/ipp/print"
    let printer = new Printer(url);
    let msg = {
        "operation-attributes-tag": {
            "document-format": "image/jpeg",
        },
        data: Buffer.from(imgBuff) ,
      };
​
axios
    .post(url, printer.encodeMsg("Print-Job",msg), {
        headers: printer.getHeaders(),
    })
    .then((response) => {
        console.log(response)
    });
​
```

​

## License

​
MIT
