go-ses - send email using Amazon AWS Simple Email Service
=========================================================

go-ses is an API client library for Amazon AWS [Simple Email Service
(SES)](http://aws.amazon.com/ses/). It is a fork of Patrick Crosby's
[stathat/amzses](https://github.com/stathat/amzses).

Note: the public API is experimental and subject to change until further notice.


Usage
=====

See full package documentation at
[godoc.org](http://godoc.org/github.com/sourcegraph/go-ses) and
[SourceGraph](https://sourcegraph.com/repos/github.com/sourcegraph/go-ses).

Example: [example_test.go](https://github.com/sourcegraph/go-ses/blob/master/example_test.go) ([SourceGraph](https://sourcegraph.com/repos/github.com/sourcegraph/go-ses/tree/master/example_test.go)):

```go
package ses_test

import (
	"fmt"
	"github.com/sourcegraph/go-ses"
)

func Example() {
	// Change the From address to a sender address that is verified in your Amazon SES account.
	from := "notify@sourcegraph.com"
	to := "success@simulator.amazonses.com"

	// EnvConfig uses the AWS credentials in the environment variables $AWS_ACCESS_KEY_ID and
	// $AWS_SECRET_ACCESS_KEY.
	res, err := ses.EnvConfig.SendEmail(from, to, "Hello, world!", "Here is the message body.")
	if err == nil {
		fmt.Printf("Sent email: %s...\n", res[:32])
	} else {
		fmt.Printf("Error sending email: %s\n", err)
	}

	// output:
	// Sent email: <SendEmailResponse xmlns="http:/...
}
```


Running tests
=============

1. Set the environment variables `$AWS_ACCESS_KEY_ID` and `$AWS_SECRET_ACCESS_KEY`.
2. Run `go test -from=user@example.com`, where `user@example.com` is a sender address that is verified
   in your Amazon SES account.


Contributors
============

* Quinn Slack <sqs@sourcegraph.com>
* Patrick Crosby (author of original [stathat/amzses](https://github.com/stathat/amzses))


Changelog
=========

2013-06-11 (forked from [stathat/amzses](https://github.com/stathat/amzses))
* renamed API functions to be consistent with AWS SES API endpoints
* reads AWS credentials from a Config struct, not from a config file
* added runnable [example_test.go](https://github.com/sourcegraph/go-ses/blob/master/example_test.go)
