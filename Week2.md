# File Object

FileReader is an object with the sole purpose of reading data from Blob (and hence File too) objects. It delivers the data using events as reading from disk may take time.

The main method is as follows:

**readAsArrayBuffer(blob)** – read the data in binary format ArrayBuffer.
**readAsText(blob, [encoding])** – read the data as a text string with the given encoding (utf-8by default).

**readAsDataURL(blob)** – read the binary data and encode it as base64 data url.
**abort()** – cancel the operation.

As the reading proceeds, there are events:

loadstart – loading started.

progress – occurs during reading.

load – no errors, reading complete.

abort – abort() called.

error – error has occurred.

loadend – reading finished with either success or failure.

When the reading is finished, we can access the result as:

reader.result is the result (if successful).

reader.error is the error (if failed).

## Fetch
The fetch() method is modern and versatile, so we’ll start with it. It evolved for several years and continues to improve, right now the support is pretty solid among browsers.

The basic syntax is:

let promise = fetch(url, [options])

url – the URL to access.

# Post request
To make a POST request, or a request with another method, we need to use fetch options:

method – HTTP-method, e.g. POST,
body – one of:
a string (e.g. JSON),
FormData object, to submit the data as form/multipart,
Blob/BufferSource to send binary data,
URLSearchParams, to submit the data in x-www-form-urlencoded encoding, rarely used

# FormData Methods
We can modify fields in FormData with methods:

formData.append(name, value) – add a form field with the given name and value,
formData.append(name, blob, fileName) – add a field as if it were <input type="file">, the third argument fileName sets file name (not form field name), as it it were a name of the file in user’s filesystem,
formData.delete(name) – remove the field with the given name,
formData.get(name) – get the value of the field with the given name,
formData.has(name) – if there exists a field with the given name, returns true, otherwise false
A form is technically allowed to have many fields with the same name, so multiple calls to append add more same-named fields.

There’s also method set, with the same syntax as append. The difference is that .set removes all fields with the given name, and then appends a new field. So it makes sure there’s only field with such name:

formData.set(name, value),
formData.set(name, blob, fileName).

# Fetch: Cross-Origin Requests
The core concept here is origin – a domain/port/protocol triplet.

Cross-origin requests – those sent to another domain (even a subdomain) or protocol or port – require special headers from the remote side. That policy is called “CORS”: Cross-Origin Resource Sharing.

For instance, let’s try fetching http://example.com:

try {

  await fetch('http://example.com');

} catch(err) {

  alert(err); // Failed to fetch

}

Fetch fails, as expected.


# Fetch: Cross-Origin Requests 
Same-Origin Policy: By default, web browsers enforce the Same-Origin Policy, which means a web page can only make requests to the same domain (protocol, hostname, and port) from which it was served. Any attempts to make cross-origin requests are blocked.

Cross-Origin Requests: Cross-origin requests occur when a web page running at one origin (e.g., https://example.com) makes a request to a different origin (e.g., https://api.example2.com).

CORS Headers: To enable cross-origin requests intentionally, a web server can include specific HTTP headers in its responses. These headers are part of the Cross-Origin Resource Sharing (CORS) mechanism.

Access-Control-Allow-Origin: This header specifies which origins are allowed to access the resource. It can be set to "*" (allowing any origin), a specific origin, or a list of origins.

Access-Control-Allow-Methods: This header specifies the HTTP methods (e.g., GET, POST, PUT, DELETE) that are allowed when making a cross-origin request.

Access-Control-Allow-Headers: This header lists the HTTP headers that the client is allowed to include with the request.

Access-Control-Allow-Credentials: This header indicates whether the browser should include credentials (like cookies or HTTP authentication) in the cross-origin request.

Access-Control-Expose-Headers: This header lists the response headers that the browser is allowed to access.

Handling CORS in Web Development:

Client-Side: When making requests from JavaScript running in a web page, you may encounter CORS restrictions. To handle this, you can use techniques like JSONP, CORS-enabled libraries (e.g., Axios), or utilize server-side proxies to forward requests to the target domain.

Server-Side: If you control the server receiving the requests, you can configure it to include the necessary CORS headers. This depends on the server technology you're using (e.g., Node.js with Express, Apache, Nginx, etc.). 

# Patterns and Flags

Pattern Definition: A regular expression pattern is a sequence of characters that defines a search pattern. It can consist of various elements, including literal characters, metacharacters, and quantifiers.
Literal Characters: Literal characters in a pattern match themselves exactly. For example, the pattern "cat" matches the string "cat" in the input text.
Metacharacters: Metacharacters are special characters with reserved meanings within regular expressions. Common metacharacters include:
. (dot): Matches any character except a newline.
* (asterisk): Matches zero or more occurrences of the preceding element.
+ (plus): Matches one or more occurrences of the preceding element.
? (question mark): Matches zero or one occurrence of the preceding element.
[] (square brackets): Defines a character class for matching any one of the characters inside.
() (parentheses): Groups elements together for applying quantifiers or other operations.
| (pipe): Represents an OR operation, allowing multiple patterns to be matched.
^ (caret): Matches the start of a line or string.
$ (dollar sign): Matches the end of a line or string.
Quantifiers: Quantifiers control how many times an element can occur in the input text. Examples include * (zero or more), + (one or more), and ? (zero or one).

Flag Definition: Flags are modifiers that can be appended to a regular expression pattern to change how the pattern is applied during matching. Flags are typically specified after the closing delimiter of the regular expression (e.g., /pattern/flags in JavaScript).
Common Flags:
i (Case-Insensitive): Matches characters regardless of case. For example, /abc/i matches "ABC," "abc," and "AbC."
g (Global): Matches all occurrences of the pattern in the input text, not just the first one.
m (Multiline): Modifies the behavior of ^ and $ to match the start and end of each line within the input text, not just the entire string.
s (Single-Line or Dot-All): Allows . to match newline characters as well.
u (Unicode): Enables full Unicode matching support.
y (Sticky): Requires the next match to start exactly at the end of the previous match.
Flags are language-specific, and not all flags are available in all programming languages.