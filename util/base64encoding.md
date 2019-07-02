# Base64 encoding

To encode a string to Bas64, just use the native btoa() function
```
var encoded = btoa("hello"); // stores "aGVsbG8=" in encoded
```
To de decode a Base64 encoded string, just use the nativ atob() function
```
var decoded = atob("aGVsbG8="); // stores "hello" in decoded
```
