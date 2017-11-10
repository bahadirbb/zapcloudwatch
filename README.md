# Cloudwatch hooks for zap

## Example

``` go
package main

import (
	"github.com/bahadirbb/zapcloudwatch"
	"go.uber.org/zap"
)

func main() {
	logger, _ := zap.NewProduction()

    hook, err := zapcloudwatch.NewCloudwatchHook().GetHook()
    if err != nil {
        panic("Failed")
    }
	// Send a notification to slack at only error, fatal, panic level
	logger = logger.WithOptions(
		zap.Hooks(hook),
	)

	logger.Debug("don't need to send a message")
	logger.Error("an error happened!")
}
```

## Install

```
$ go get -u github.com/bahadirbb/zapcloudwatch
```

This is a mixin project from these 2 repositories
https://github.com/bluele/zapslack
https://github.com/kdar/logrus-cloudwatchlogs

## Author

**Bahadir Bozdag**

* <http://github.com/bahadirbb>
* <bahadirbb@gmail.com>