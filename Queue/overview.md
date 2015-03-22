{{{
  "title": "Queue API Overview",
  "date": "10-13-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

Many operations performed by the API are actually long running tasks, for example creating a new server, or creating a new website in the Web Farm. As a result, these tasks are performed asynchronously. All of the operations which need to be processed asynchronously will return a `RequestID` property in their responses. The Queue API allows you to query into the queue to get the status of your requests using this `RequestID`. Many of these operations also send email notifications upon completion.

The URL to the SOAP version of the Queue API can be found at [https://api.ctl.io/soap/Queue.asmx](https://api.ctl.io/soap/Queue.asmx) and the WSDL can be found [here](https://api.ctl.io/soap/Queue.asmx?wsdl).
