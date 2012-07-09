amzses
======

This is a Go package to send emails using Amazon's Simple Email Service.

Installation
------------

Use `go get`:

    go get github.com/alltom/amzses

If you are building your code with `goinstall`, you can skip the previous step and just
import `amzses` as follows:

    import (
            "github.com/alltom/amzses"
    )

Using `go install` will automatically install its one external dependency,
[jconfig](http://www.stathat.com/src/jconfig).

Usage
-----

Optionally, save your credentials in `/etc/aws.conf`:

    {
        "aws_access_key": "XXX_YOUR_ACCESS_KEY_XXX",
        "aws_secret_key": "YYY_YOUR_SECRET_KEY_YYY"
    }

Then create and use an ses object:

    ses := amzses.Init() // credentials loaded from /etc/aws.conf
    ses := amzses.InitAuth("XXX_YOUR_ACCESS_KEY_XXX", "YYY_YOUR_SECRET_KEY_YYY")
    
    _, err := ses.SendMail("info@example.com", "user@gmail.com", "Welcome!", "Welcome to our project!\n\n...")

The first return value is the response string from the server. To extract the message and request IDs:

    var resp amzses.AmazonResponse
    err := xml.Unmarshal([]byte(s), &resp)
    // resp.MessageId, resp.RequestId

Status
------

The modifications in this fork (alltom/amzses) haven't really been tested at all, but
the original library (stathat/amzses) was in use at StatHat in production, so it's
probably in pretty good shape.

About
-----

The original library was written by Patrick Crosby at [StatHat](http://www.stathat.com).
Twitter: [@stat_hat](http://twitter.com/stat_hat)
