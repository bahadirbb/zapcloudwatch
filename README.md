# Cloudwatch hook for zap

## Example

``` go
package main

import (
	"github.com/bahadirbb/zapcloudwatch"
	"go.uber.org/zap"
)

func getLogger(name string) *zap.Logger {

	cred := credentials.NewStaticCredentials(awsAccessKey, awsSecretKey, "")
	cfg := aws.NewConfig().WithRegion(awsRegion).WithCredentials(cred)

	cloudwatchHook, err := zapcloudwatch.NewCloudwatchHook("xyz", "xyz1", false, cfg, zapcore.InfoLevel).GetHook()
	if err != nil {
		panic(err)
	}

	config := zap.NewDevelopmentConfig()
	config.Encoding = "json"
	logger, _ := config.Build()
	logger = logger.WithOptions(zap.Hooks(cloudwatchHook)).Named(name)
	return logger
}

func main() {
	logger, _ := getLogger("test")

	logger.Debug("don't need to send a message")
	logger.Error("an error happened!")
}
```

## Install

```
$ go get -u github.com/bahadirbb/zapcloudwatch
```

This is a mixin project from these 2 repositories. 
Warning as a zaphook this hook doesn't log fields. If you need complete logging with fields don't use this hook. You need to implement zap.Core


https://github.com/bluele/zapslack

https://github.com/kdar/logrus-cloudwatchlogs

## Author

**Bahadir Bozdag**

* <http://github.com/bahadirbb>
* <bahadirbb@gmail.com>