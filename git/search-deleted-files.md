# Search deleted files 

```shell
$ git log -p --all --full-history -- **/credentials.go

commit f5ff0a9495c222c938ded97f874f1d687a32e6bd
Author: Mario Castro <REDACTED>
Date:   Fri Jul 22 17:43:42 2022 +0200

    [Feature Branch] Upgrade AWS SDK v2 library to the latest version (#31224)

diff --git a/x-pack/libbeat/common/aws/credentials.go b/x-pack/libbeat/common/aws/credentials.go
index f7d2e90951..0467c02df2 100644
--- a/x-pack/libbeat/common/aws/credentials.go
+++ b/x-pack/libbeat/common/aws/credentials.go
@@ -5,18 +5,21 @@
 package aws

 import (
+       "context"
        "crypto/tls"
        "fmt"
        "net/http"
        "net/url"
        "strings"

-       awssdk "github.com/aws/aws-sdk-go-v2/aws"
-       "github.com/aws/aws-sdk-go-v2/aws/defaults"
-       "github.com/aws/aws-sdk-go-v2/aws/external"
-       "github.com/aws/aws-sdk-go-v2/aws/stscreds"
        "github.com/aws/aws-sdk-go-v2/service/sts"

+       "github.com/aws/aws-sdk-go-v2/credentials/stscreds"
+
```
