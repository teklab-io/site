### Status codes

See [https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) and [https://tools.ietf.org/html/rfc4918](https://tools.ietf.org/html/rfc4918).


| Problem | Status Code | Status Text |
| ------- | ----------- | ----------- |
| The client submitted structurally **invalid** request (e.g. JSON doesn't parse) | 400  | Bad Request | 
| The client submitted a valid request without any authorization credentials (e.g. token) | 401 | Unauthorized |
| The client submitted a structurally valid result but the user doesn't have permissions to do an action | 403 | Forbidden | 
| The client submitted a structurally valid request but business logic constraint that is specifically related to the lifecycle of the entity meant that it could not happen (e.g. tried to order something twice) | 409 | Conflict | 
| The client submitted a structurally valid request but someone else has made a request in the meantime that conflicts (can be checked for with a conditional request) | 409 | Conflict |
| The client submitted a structurally valid request but a general business logic constraint meant that it could not happen (e.g. No funds in your account)  | 422 | Unprocessable Entity | 
| The client submitted a structurally valid request but the request is refused due to an indirect business constraint (e.g. fraud / credit rating check) | 422 | Unprocessable entity |
| The client submitted a structurally valid request but it failed basic validation] (e.g. A date failed validation)| 422 | Unprocessable entity |
|  The client submitted a structurally valid request but some downstream dependant business action failed, as opposed to a technical failure (e.g. An order service depends on an inventory service and stock items are not available) | 424 | Failed dependency | 

**Response messages**

Don't only rely on the status codes, always return a message in the body, with a known media type. For example if you are building a JSON api, return a JSON structure. Providing more information in situ is going to be useful for developers coding against your api. 

Use hyperlinks in the response to documentation about the error and why it might have occured along with a short description.

Provide specific, structured details where appropriate, e.g.:

    {
      error: {
        type: field-validation
        code: 43	
        message: { id: 223, en_gb: "We were unable to interpret the data in one or more fields" }
        doc: http://...  
        fields: [
          dateOfBirth: {
             message: { id: 223:43 en_gb: "[foo/bar/20] could not be recognised as a valid date."}
             invalidData: "foo/bar/20"
             requiredFormat: "dd/mm/yyyy"
             doc: http://...
          }
        ]
      }
    }

The structure of the message allows clients to either use it directly or map to their own set of translations / custom messages. 

**WebDav**

422 and 424 both derive from the WebDav RFC ([RFC4918](https://tools.ietf.org/html/rfc4918)). If you wanted to remain within the HTTP core spec, you could replace them both with a generic 400.

**Security**


There is a separate discussion to be had about wether or not this is a security risk, which might depend a lot on the context of the calling client (how much we trust it) and how available the documentation is online. 

This section needs some thought. If you are building a public API then your going to publish your documentation anyway. Theres a tradeoff between obfuscating for "security" vs getting people to love your api. If your really paranoid then probably the best thing is just return 400 and a generic error message such as:

{
  error
}

If you are concerned about providing too much information to a potential hacker, replace (401 and 403) with 404 - Not Found.

**Interaction Modelling**

Use of the code 422 falls on the border between structural and protocol levels and business process levels. It could be argued that these responses should not be modelled with HTTP status codes (which are more focused at the protocol level). However, pragmatically many APIS expose synchronous "RPC" style interfaces which may fail for one of these reasons, and if you consider it useful to distinguish between these kinds of respons at the HTP level, then 422 is a reasonable approach. An alternative is to just use 400 for everything.


